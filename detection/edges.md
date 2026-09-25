(P:edge-detection)=
# Edge detection


An edge (French: *contour*) in an image is the frontier that delimits two objects.
Therefore, edge detection is useful for identifying or measuring objects, or segmenting the image.

<!------------------------------------------------------------------------------------------------>

## The advantage of using the derivatives

Edges are characterized by a rapid variation in the intensity of the pixels.
@F:detection:profile represents the brightness profile along a horizontal line in the image.
One clearly sees that the outline of the industrial piece shows a sudden decrease in the brightness of the pixels.

:::{figure} figs/edges-profile.svg
:name: F:detection:profile
An image and the luminosity profile on it.
:::

From this example, it appears that derivation is an efficient tool for highlighting the edges:
an edge can be detected by analyzing the first derivative of the intensity profile,
taken perpendicular to the edge.
Similarly, an edge can be detected by determining the zero-crossing of the second derivative.

:::{figure} figs/edges-derivatives.svg
:name: F:detection:derivatives
The profile of @F:detection:profile and its derivatives.
:::

Because an image depends on two dimensions, the derivatives must be calculated according to the two axes.
In addition, the derivatives are discrete differences in the case of digital images.
Then, the first derivative of a digital image $f$ are defined as:

$$
\frac{\partial f(y,x)}{\partial x} &= f(y,x+1) - f(y,x) \\
\frac{\partial f(y,x)}{\partial y} &= f(y+1,x) - f(y,x).
$$

<!-- (image représentant le gradient, GW p.729) -->

The first derivatives are gathered in the so-called "gradient" (French: *gradient*) defined as:

$$
\nabla f =
\begin{pmatrix}
  f(y,x+1) - f(y,x) \\ f(y+1,x) - f(y,x)
\end{pmatrix}
$$

In the same way, the second derivative, called "Laplacian" (French: _laplacien_), is defined as:

$$
\Delta f =
\begin{pmatrix}
  f(y,x+1) - 2f(y,x) + f(y,x-1) \\ f(y+1,x) - 2f(y,x) + f(y-1,x)
\end{pmatrix}
$$

<!------------------------------------------------------------------------------------------------>

## Gradient operators

Gradient operators are very simple methods for detecting edges.
They use the first derivative and can be calculated by using a convolution.
Indeed, the first derivative along the $x$ axis of an image $f$ can be written as a convolution product:

$$
f(y,x+1) - f(y,x) = \sum_m \sum_n f(y-m,x-n) \ h_x(m,n) 
$$

where $h_x$ is a convolution kernel such that:

* $h_x(0,-1) = +1$,
* $h_x(0,0) = -1$,
* and $h_x(m,n) = 0$ elsewhere.

Thus, the kernel $h_x$ is (the origin $(0,0)$ is the pixel with value $-1$):

$$
h_x =
\begin{pmatrix}
  0  &  0 \\
  +1 & -1 \\
\end{pmatrix}
$$

Similarly, the first derivative along the $y$ axis is written as the convolution of $f$ with the kernel $h_y$:

$$
h_y =
\begin{pmatrix}
  0 & +1 \\
  0 & -1 \\
\end{pmatrix}
$$

Note that the row of 0 in $h_x$ and the column of 0 in $h_y$
allows having kernels of the same size. 
These two kernels are the very basic gradient operator
and, in practice, variants of them are used.

### Roberts operator

The Roberts operator finds the edges along the diagonals [[Roberts 1965](B:detection:Roberts1965)]:

$$
  h_x=
  \begin{pmatrix}
    +1 & 0 \\
    0 & -1 \\
  \end{pmatrix}
  \quad
  h_y=
  \begin{pmatrix}
    0 & +1 \\
    -1 & 0 \\
  \end{pmatrix}
$$


### Prewitt operator

The Prewitt operator [[Prewitt 1970](B:detection:Prewitt1970)]
use kernels with odd sizes, so as to get a detection centered on the edges:

$$
  h_x=
  \begin{pmatrix}
    +1 & 0 & -1 \\
    +1 & 0 & -1 \\
    +1 & 0 & -1 \\
  \end{pmatrix}
  \quad
  h_y=
  \begin{pmatrix}
    +1 & +1 & +1 \\
    0 & 0 & 0 \\
    -1 & -1 & -1 \\
  \end{pmatrix}
$$


(P:detection:sobel)=
### Sobel operator

The Sobel operator [[Sobel 1968](B:detection:Sobel1968)]
can be seen as a smoothed version of the Prewitt operator.
Indeed, the coefficients reproduce a convolution by a Gaussian filter,
which tends to play the role of a mean filter to attenuate noise:

$$
  h_x=
  \begin{pmatrix}
    +1 & 0 & -1 \\
    +2 & 0 & -2 \\
    +1 & 0 & -1 \\
  \end{pmatrix}
  \quad
  h_y=
  \begin{pmatrix}
    +1 & +2 & +1 \\
    0 & 0 & 0 \\
    -1 & -2 & -1 \\
  \end{pmatrix}
$$

Note that the sum of the elements is zero, as with the Roberts and Prewitt operators.

In @F:detection:sobel-h-v, one can see that $h_x$ detects vertical edges.
For example, the left and right of the clock are clearly detected.
The left edge is white because it corresponds to an edge from black to white.
On the contrary, the right edge is black.
On the other side, $h_y$ detects horizontal edges.

:::{figure} figs/sobel-h-v.svg
:name: F:detection:sobel-h-v
Horizontal and vertical Sobel operator.
:::


### Magnitude and angle

From the operators above, we also define:

* the magnitude of the edge, which can be interpreted as the "fusion" of the horizontal and vertical Sobel operator:

  $$
  M = \sqrt{ (h_x*f)^2 + (h_y*f)^2 }
  $$
  
  In @F:detection:sobel-magnitude-angle, all the edges appear with the same color, whatever their orientation.

* the angle of the edge:
  
  $$
  A = \arctan \left( \frac{h_y*f}{h_x*f} \right)
  $$
  
  In @F:detection:sobel-magnitude-angle, the color of the edges corresponds to the edge orientation.
  Especially, verticals are in red, and horizontals in cyan.

:::{figure} figs/sobel-magnitude-angle.svg
:name: F:detection:sobel-magnitude-angle
Magnitude and angle of the Sobel operator.
:::


### Thresholding

In some cases, it would be useful to detect the most important edges.
To do that, one can threshold the magnitude to keep only the large values of the gradients.
As you can see in @F:detection:sobel-magnitude-threshold, the threshold makes the second hand disappear.
Indeed, the magnitude is lower than other parts of the image because the second hand is gray and not black.

:::{figure} figs/sobel-magnitude-threshold.svg
:name: F:detection:sobel-magnitude-threshold
Thresholding the magnitude of the Sobel operator makes the second hands disappear!
:::


### The impact of noise

Noise in an image essentially brings great variations in brightness between pixels.
Therefore, the gradient operator, which are based on the derivative,
are very sensitive to the noise (see @F:detection:edges-derivatives-noise).
Then it may be useful to denoise the image before edge detection.

:::{figure} figs/edges-derivatives-noise.svg
:name: F:detection:edges-derivatives-noise
Consequence of noise on the brightness profile and its derivatives
(orange: non-noisy profiles, blue: noisy profiles).
:::

In @F:detection:edges-sobel-noise, a small [blur filter](P:filtering:blur-filter) is used before the Sobel filter:
the result is much cleaner than without the use of the mean filter.

:::{figure} figs/edges-sobel-noise.svg
:name: F:detection:edges-sobel-noise
Left: noisy image.
Center: Sobel operator (magnitude).
Right: Sobel operator applied on the result of a 3×3 mean filter.
:::

<!------------------------------------------------------------------------------------------------>

## Advanced methods

Following the gradient operator, new methods have been proposed to improve edge detection
by taking into account the noise and the nature of the edges:
* the Marr-Hildreth detector [[Marr & Hildreth 1980](B:detection:Marr1980)],
* the Canny detector [[Canny 1986](B:detection:Canny1986)].


### Marr-Hildreth Detector

<!-- Hypotèses~:
  \item Un contour doit être détecté quelle que soit l'échelle de l'image \\
  \uncover<3>{=> le détecteur doit être réglable pour détecter les contours à une échelle particulière.}
  \item Un contour implique un passage par zéro de la dérivée 2\textsuperscript{e} \\
  \uncover<3>{=> le détecteur doit calculer la dérivée 2\textsuperscript{e}.} -->

The Marr-Hildreth detector consists of:
1. applying a Gaussian filter $g$ on the image $f$ to reduce noise (this is similar to a mean filter), leading to an image $g*f$,
2. computing the Laplacian (second derivative) $\ell$ on the softened image (this is implemented with a convolution),
3. determining the zero-crossings of the result.

As $\ell*(g*f) = (\ell*g)*f$, the first two steps are merged into a single convolution by $\ell*g$.
The filter $\ell*g$ is the second derivative of a Gaussian:

$$
  (\ell*g)(y,x) = - \left[\frac{y^2+x^2-2\sigma^2}{\sigma^4}\right] \exp\left(-\frac{y^2+x^2}{2\sigma^2}\right).
$$

The filter $\ell*g$ is represented @F:detection:log.
It is also called "LoG" for Laplacian of Gaussian (no French equivalent) or Mexican hat (for the resemblance to a sombrero).

:::{figure} figs/log.svg
:name: F:detection:log
Laplacian of Gaussian (left: as an image, right: profile along an axis).
:::

The zero-crossings in the image resulting from the LoG convolution are given by searching for changes of sign in the intensity of two pixels.

@F:detection:marr-hildreth gives an example of applying the Marr-Hlidreth detector.

:::{figure} figs/moulinsart-marr-hildreth.svg
:name: F:detection:marr-hildreth
Marr-Hildreth Detector.
Left: original image,
center: result of the LoG filter,
right: detection of the zeros crossings.
:::

:::{figure} figs/caramba-marr-hildreth.svg
:width: 3px
:name: F:detection:caramba
:::

:::{note}
Marr and Hildreth note that it is possible to approximate the LoG filter
by a difference of Gaussians (DoG) with $\sigma_1 > \sigma_2$
[[Gonzalez 2010](B:detection:Gonzalez2010)].

$$
\mathrm{DoG}(y,x)
= \frac{1}{2\pi\sigma_1^2}\exp\left(-\frac{x^2+y^2}{2\sigma_1^2}\right)
- \frac{1}{2\pi\sigma_2^2}\exp\left(-\frac{x^2+y^2}{2\sigma_2^2}\right)
$$
:::


### Canny Detector

According to Canny, a good detector should serve the following purposes:
* all edges should be found,
* there should be a minimum of spurious responses,
* the edges must be correctly localized (_i.e._ the distance between a detected point and the true point of the edge must be as small as possible),
* the thickness of the detected edges must be 1 pixel (therefore only one point must be detected for each true point of the edge).

Canny expressed these goals in mathematical form and came up with optimal solutions verifying these goals.
The Canny detector algorithm follows the four steps detailed below.

<!-- TODO : présenter l'algo avec des illustrations et des schémas -->

1. The image $f$ is first smoothed with a Gaussian filter to reduce noise.
    This is done by using a convolution with a Gaussian kernel $g$ to obtain an image $z = f*g$.

2. The gradient of the image is calculated (amplitude and angle):

   $$
   M = \sqrt{ (h_x*z)^2 + (h_y*z)^2 }
   \quad\text{and}\quad
   A = \arctan \left( \frac{h_y*z}{h_x*z} \right)
   $$
   
3. Non-maxima are removed from the amplitude.
   This means that excessively large outlines in $M$ are replaced by thinner outlines.
   For this, we apply the algorithm below:
   
    :::{card}
    1. For each pixel $(x,y)$ in $M$:
       1. Choose the direction (vertical, horizontal or one of the two diagonals) the closest to $A(x,y)$
       1. If $M(x,y)$ is lower than one of its neighbors in the chosen direction then cancel the gradient: $M(x,y)=0$
    :::

4. The last step consists of thresholding by hysteresis for the bad edges.
   Two thresholds are therefore defined ($T_\text{high} > T_\text{low}$) and the algorithm below is applied:
      
    :::{card}
    1. For each pixel $(x,y)$ in $M$:
       1. If $M(x,y) > T_\text{high}$                 then $(x,y)$ is an edge
       1. If $T_\text{low} < M(x,y) < T_\text{high}$  then $(x,y)$ is an edge if and only if it is neighbor of an edge pixel 
       1. If $M(x,y) < T_\text{low}$                  then $(x,y)$ is not an edge
    :::
   
@F:detection:canny gives an example of Canny edge detection.

:::{figure} figs/moulinsart-canny.svg
:name: F:detection:canny
Canny Detector.
:::


### Comparison

@F:detection:sobel-marr-hildreth-canny shows the results of the Sobel, Marr-Hildreth and Canny detectors on an image.
A detail is given in @F:detection:marr-hildreth-canny
and compares Marr-Hildreth and Canny detectors:
one can see that the edges detected with Canny detector are better localized.

:::{figure} figs/sobel-marr-hildreth-canny.svg
:name: F:detection:sobel-marr-hildreth-canny
Comparison of Sobel, Marr-Hildreth and Canny detectors.
:::

:::{figure} figs/marr-hildreth-canny.svg
:name: F:detection:marr-hildreth-canny
Comparison between Marr-Hildreth and Canny detectors (zoom).
The edges are shown in green.
:::