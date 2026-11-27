(C:sift)=
# SIFT


The scale-invariant feature transform (SIFT) algorithm was proposed by [Lowe, 1999](#B:detection:Lowe1999)
to detect specific pixels in two images and to match them by using some descriptors that characterize them.
SIFT is still one of the most popular feature detectors today because the algorithm is robust to translation, scaling, rotation, partial occlusion or illumination changes.
Applications include object recognition, video tracking, robotic navigation, image composition (stitching), etc.

The 6 stages in SIFT are the following and they are described in the next sections.

:::{note} Scale-invariant feature transform (SIFT)
:icon: false
1. A *scale-space* with Gaussian kernel is computed so as to get a collection of images with different blur level and resolution.
1. At each resolution, a few difference-of-Gaussian are computed : they are the data to find the following *keypoints*.
1. Pixels with high intensity variation in the scale-space are detected: they are the so-called keypoints.
1. The main orientation gradient is determined in a local window centered on the keypoints.
1. Descriptors (vectors with 128 values) are computed for each keypoints.
1. Finally a matching is possible between keypoints and their descriptors of two images.
:::

:::{caution}
This page presents a simplified version of the SIFT algorithm and aims to give the main ideas of the algorithm.
Detailed specifications are given in [[Rey-Otero, 2014](#B:detection:ReyOtero2014)], for instance.
:::

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

## Scale-space representation

A *scale-space representation* is a series of images with decreasing resolution.
Each resolution is called an *octave*.

Let $f(x,y)$ be the original image and $O$ the number of octaves (typically, $O=8$).
The first image $f_0$ in the scale-space representation is the original image:

$$
f_0(x,y) = f(x,y).
$$

The image $f_o$ at octave $o\in\{1,\dots,O-1\}$ is defined as

$$
f_o(x,y) = \mathcal{D}_o \big[ f(x,y) * g(x,y,\sigma_o) \big]
$$

where:

* $\mathcal{D}_o$ is a downsampling by a factor $2^o$ by using @P:interpolation:order1.

* $g$ is a Gaussian kernel that prevents aliasing after downsampling:
  $$
  g(x,y,\sigma_o) = \frac{1}{2\pi\sigma_o^2} e^{-(x^2+y^2)/2\sigma_o^2}.
  $$
  Because the Gaussian function is [separable](#P:convolution:separability),
  the convolution can be efficiently computed by applying two passes of a 1D Gaussian function in the horizontal and vertical directions.

* $\sigma_o$ is the parameter of the Gaussian kernel and is defined as $\sigma_o = 2^{o-1} \sigma_\mathrm{min}$
  and $\sigma_\mathrm{min}$ is the blur level considered in the original image (see [[Rey-Otero, 2014](#B:detection:ReyOtero2014)]).

The series of blurred and downsampled images produces a pyramid representation,
as illustrated in @F:detection:sift:scale-space.

:::{figure} figs/image_pyramid.webp
:height: 400px
:name: F:detection:sift:scale-space
Scale space representation [Wikipedia].
:::

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

## Difference-of-Gaussian at each scale

At each octave $o$ of the scale space, $K$ blurred images are produced (typically, $K=3$).
The image $f_{o,k}$ at octave $o$ and blur level $k\in\{1,\dots,K\}$ is defined as:

$$
f_{o,k}(x,y) = \mathcal{D}_o \big[ f(x,y) * g(x,y,k\sigma_o) \big]
$$

Note that $f_{o,1}(x,y) = f_o(x,y)$.

Then, we compute the differences between two successive images:

\begin{align*}
d_{o,k}(x,y)
&= f_{o,k}(x,y) - f_{o,k-1}(x,y) \\
&= \mathcal{D}_o \big[ f(x,y) * g(x,y,k\sigma_o) \big] - \mathcal{D}_o \big[ f(x,y) * g(x,y,(k-1)\sigma_o) \big] \\
&= \mathcal{D}_o \big[ f(x,y) * g(x,y,k\sigma_o) - f(x,y) * g(x,y,(k-1)\sigma_o) \big] \\
&= \mathcal{D}_o \big[ f(x,y) * \big( \underbrace{g(x,y,k\sigma_o) - g(x,y,(k-1)\sigma_o)}_\mathrm{DoG} \big) \big] \\
\end{align*}

where $g(x,y,k\sigma_o) - g(x,y,(k-1)\sigma_o)$ is called the *difference-of-Gaussian* (DoG) and acts as a bandpass filter.

:::{figure} figs/sift-DoG.png
:width: 100%
:name: F:detection:sift:DoG
Scale space and DoG at each octave and for each couple of blurred images [[Lowe 2004](#B:detection:Lowe2004)].
:::

:::{figure} figs/sift-DoG-appli.png
:width: 100%
:name: F:detection:sift:DoG-appli
Example of DoG scale-space on an image (left).
[[Rey Otero 2014](#B:detection:ReyOtero2014)].
:::

% Illustration du DoG (en particulier sur une ellipse : cf Lowe2004, fin de la p.95

% lien avec le Laplacien : cf Lowe2004, section 3

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

## Keypoint detection

*Keypoints* are defined as pixels in the image that are invariant to scale and orientation.
To detect keypoints, each pixel in a blurred image (at each octave and scale)
is compared to its 8 neighbors in the current image
and its 18 neighbors in the scale above and below (@F:detection:sift:DoG-extrema).
This gives a total of 26 neighbors.

:::{figure} figs/sift-extrema.png
:height: 200px
:name: F:detection:sift:DoG-extrema
Extrema of the DoG images are detected by comparing a pixel (marked with $\times$)
to its neighbors (marked with circles) at the current and adjacent scales
[[Lowe 2004](#B:detection:Lowe2004)].
:::

The pixel is then considered as a keypoint if and only if it is an extremum in its neighboring,
i.e. it is greater or smaller than all of its neighbors.
Note that some detected keypoints are discarded if they are low contrasted
or if they lie on an edge (because their localization cannot be precise enough along the edge).

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

## Keypoints orientations

Each remaining keypoint is assigned to an orientation so that the descriptors are invariant to rotation.

In order to make the orientation as stable as possible against lighting or contrast changes,
the orientation is not the gradient angle but is determined from *histogram of oriented gradient* (HOG).
HOG is simply the histogram of the gradient angles in a window around the keypoint:
each pixel in the window contributes to the histogram by adding a value equal to the gradient magnitude
to the (nearest) bin corresponding to the gradient orientation (@F:detection:sift:HoG).

:::{figure} figs/sift-hog.svg
:height: 300px
:name: F:detection:sift:HoG
HoG on a 160×160 image.
Each window is of size 16×16.
:::

In SIFT, the histogram has 36 bins covering the 360 degree range of rotations.
The orientation to assign to the keypoint is determined by the highest peak in the histogram.

:::{figure} figs/sift-keypoints.svg
:height: 300px
:name: F:detection:sift:keypoints
Keypoints and their orientation.
:::

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

## Keypoints descriptors

A descriptors is, generally, a list of numerical values that characterize the keypoint.
This stage consists in computing a descriptor for the local region around each keypoint,
so that the desciptor is as invariant as possible to remaining variations, such as change in illumination or 3D viewpoint.

Again, the magnitude and angle of the gradient is used to define the desciptor.
So, a 16×16 window centered on the keypoint is defined,
furthermore it is oriented relative to the keypoint orientation in order to be invariant in rotation (@F:sift:keypoints-and-windows).

:::{figure} figs/sift-keypoints-and-windows.svg
:height: 250px
:name: F:sift:keypoints-and-windows
Keypoints, their orientation, and their windows where an HoG is computed.
:::

The 16×16 window is divided into 16 cells where an HoG is computer with 8 orientation bins in each.
The descriptor is the vector containing the values of all the orientation histogram entries,
therefore, it contains 16 cells × 8 bins = 128 features.

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

## Matching

The final stage of SIFT is to find matching between the descriptors of one image with the descriptors of a second image.
To do that, the descriptors are considered as points in a 128-dimensional space.
The goal is to find the lowest Eclidean distance between the points.
The descriptor $d_i^1$ of image 1 is paired to the descriptor $d_j^2$ of image 2 that minimizes the Euclidean distance between descriptors.
A pair is considered reliable only if its distance is below a certain threshold, otherwise it is discarded.

This matching problem considered the pairing of, typically, thousands of descriptors in a high dimensional space:
it is known to have high complexity if an exact solution is required.
Instead, a modification of the k-d tree algorithm called the best-bin-first search method is used to identify the nearest neighbors with high probability,
using only a limited amount of computation.

@F:sift:arc shows an example of matching.

:::{figure} figs/sift-arc.svg
:width: 100%
:name: F:sift:arc
Example of matching on the main paired keypoints.
:::

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

## Alternatives to SIFT

SURF (Speeded-Up Robust Features) [[Bay 2006](#B:detection:Bay2006)] accelerates SIFT
so it is more suitable for real-time applications.
The main differences with SIFT are the following:

* _Integral images_ are used to deal with convolutions.
  An integral image $I$ represents the sum of all pixels in the input image $f$
  that are in the rectangular region formed by the origin and the pixel in $I$:
  
  $$
  I(x,y) = \sum_{m=0}^{x} \sum_{n=0}^{y} f(m,n).
  $$

* DoG approximates a second derivative (or Laplacian, which is actually the trace of the Hessian matrix).
  SURF replaces DoG by a fast approximation of the Hessian matrix.

* The orientation of the keypoints are determinated with _Haar wavelets_,
  which are a series of binary masks with rectangular regions.

* Other modifications simplify the different stages of the SIFT algorithm to the essential.
  For instance, SURF produces a 64-dimensional descriptor, which is more compact and faster to compute than SIFT descriptor.

ORB (Orientated FAST and Robust BRIEF) [[Rublee 2011](#B:detection:Rublee2011)]
is considered to be roughly 10 times faster than SURF, while performing as well in many situations.

% https://mikhail-kennerley.medium.com/a-comparison-of-sift-surf-and-orb-on-opencv-59119b9ec3d0


% À ranger

% https://www.micc.unifi.it/delbimbo/wp-content/uploads/2011/03/slide_corso/A33%20SIFT-GLOH-SURF.pdf
% https://github.com/hoanglehaithanh/Traffic-Sign-Detection
% https://github.com/mohd-adeeb011/Traffic-Sign-Board-Recognition-Using-Camera
% https://www.geeksforgeeks.org/computer-vision/what-is-the-difference-between-sift-and-surf/
% https://scikit-image.org/docs/0.25.x/auto_examples/features_detection/plot_brief.html
% https://scikit-image.org/docs/0.25.x/auto_examples/features_detection/plot_orb.html