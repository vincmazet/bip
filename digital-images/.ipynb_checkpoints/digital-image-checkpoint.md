# What is a digital image?


## Definition

```{margin}
In very specific applications, the images may have a non-rectangular geometry.
For example, some sensors have hexagonal pixels.
We will not deal with this kind of image as it is very rare.
```

A digital image can be seen as a function $f$ from $\mathbb{N}^d$ to $\mathbb{R}^B$:
it associates at each discrete coordinate $(m,\,n,\,\dots) \in \mathbb{N}^d$
a finite set of intensities $\{i_1,\dots,i_B\} \in \mathbb{R}^B$.


$$
\begin{aligned}
  f:\qquad\;
  \mathbb{N}^d &\to \mathbb{R}^B \\
  m,n,\dots    &\mapsto f(m,n,\dots) = \{i_1,\dots,i_B\}.
\end{aligned}
$$

A digital image can also be seen as an array of $d$ dimensions whose elements contain $B$ numbers.

For example, a [grayscale image](https://en.wikipedia.org/wiki/Grayscale) corresponds to $d=2$ (the image has two dimensions) and $B=1$ (there is only one value per location $(m,n)$: the grayscale intensity).
A common color image corresponds to $d=2$ and $B=3$ (there are three bands: red, green, blue).
An [MRI image](https://en.wikipedia.org/wiki/Magnetic_resonance_imaging) corresponds to $d=3$ (the image is three-dimensional) and $B=1$.

In the general case of a 2-dimensional image $f(m,n)$ of size $M \times N$,
one uses the coordinate system showed {numref}`F:definition:coordinates`:
the pixel at coordinates $(0,0)$ is on the top left corner of the image.

```{figure} coordinates.png
---
scale: 100%
name: F:definition:coordinates
---
Coordinate system generally used in image processing.
```


## Diversity of images

Digital images can be differentiated in several ways.

### Dimension number
Common images (like photography) are 2D (2-dimensional) images whereas some other images lie in more than two dimensions.
A 3D image, like in MRI, is often called "3D image" or "cube".
A 1D image is actually a signal.
The elements constituting a 2D image are called _pixels_ (for "picture element"),
and the one constituting a 3D image are called _voxels_ (for "volume element").

### Dimension heterogeneity
In common 2D images, the two dimensions are both spatial dimensions.
But the dimensions may represent another physical domain and be different.
For example, a video can be seen as a 2D+$t$ image (two spatial dimensions, one temporal dimension),
an MRI sequence can be seen as a 3D+$t$ image (three spatial dimensions, one temporal dimension),
and a [hyperspectral image](https://en.wikipedia.org/wiki/Hyperspectral_imaging)
is a 3D+$\lambda$ image (two spatial dimensions, plus a third dimension depending on the wavelength).

### Element dimension
Each element of an image can be scalar or vector.
For example, the pixels in a 2D grayscale image gather only one value (the gray intensity).
The pixels in photography gather three values (the intensity of red, green and blue).
The images from the [Pléiades constellation](https://en.wikipedia.org/wiki/Pleiades_(satellite)) are RVB--IR,
therefore they gather four values (red, green, blue, and infrared).

### Element intensity set
Common images have pixel intensities in the range $\{0,1,\dots,255\}$,
but a binary image has values in $\{0,1\}$.
Generally, an image is considered to have intensities within the set $\{i_1,\dots,i_B\}\in\mathbb{R}^B$.


## Displaying an image

Displaying an image needs to convert the pixel intensities $\{i_1,\dots,i_B\}$ in gray levels or colors.
The correspondance between intensities and colors is visually reprensented by a _colormap_.

### Displaying a 2D grayscale image
A 2D grayscale image is an array with $d=2$ dimensions where each pixel contains a scalar ($B=1$).
Therefore, each pixel is displayed with a specific gray level.
{numref}`F:definition:colormap` shows the same image with different colormaps.
As you can see, the choice of the colormap changes the perception of the colors,
even if the information contained by the pixels remains the same.

```{figure} ../figs/colormaps.svg
---
name: F:definition:colormap
---
An image showing Buzz Aldrin displayed with the colormaps given below the images.
```

**+ échelle log**


### Displaying a 2D color image

```{margin}
[A nice video](https://youtu.be/FvbNrwjIrNU).
```

The retina of human eye contains cone cells (french: _cônes_) which allow color vision
There are three types of cones which are sensitive to short, medium and longer wavelength of the visible light.
Basically, they are sensitive to blue, green and red light.
So, color images are simply a composition of the intensities of this three wavelength, so that $B=3$.
Each of this three bands codes the intensity of red, green and blue lights of the image, hence the name RGB (red, green, blue).


### Displaying other types of images
There is not an esy way to display an image which is not a 2D grayscale or RGB image.
Either this kind of image are simply not displayed, or a specific representation must be chosen.