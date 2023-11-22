(C:edge-detection)=
# Edge detection


An edge (French: _contour_) in an image is the frontier that delimits two objects.
Therefore, edge detection is useful for identifying or measuring objects, or segmenting the image.


## The advantage of using the derivatives

Edges are characterized by a rapid variation in the intensity of the pixels.
{numref}`F:detection:profile` represents the brightness profile along a horizontal line in the image.
One clearly sees that the outline of the industrial piece shows a sudden decrease in the brightness of the pixels.

```{figure} edges-profile.svg
---
width: 600px
name: F:detection:profile
---
An image and the luminosity profile on it.
```

From this example, it appears that derivation is an efficient tool for highlighting the edges:
an edge can be detected by analyzing the first derivative of the intensity profile,
taken perpendicular to the edge.
Similarly, an edge can be detected by determining the zero crossing of the second derivative.

```{figure} edges-derivatives.svg
---
width: 600px
name: F:detection:derivatives
---
The profile of {numref}`F:detection:profile` and its derivatives.
```

Because an image depends on two dimensions, the derivatives must be calculated according to the two axes.
For example, the first derivative of an image $f$ consists of the two terms
$\frac{\partial f(x,y)}{\partial x}$ and $\frac{\partial f(x,y)}{\partial y}$.
In addition, the derivatives are discrete differences in the case of digital images.

<!-- (image représentant le gradient, GW p.729) -->

Thus the first derivative, also called "gradient" (French: _gradient_), is defined by:

$$
\nabla f =
\begin{pmatrix}
  f(x+1,y) - f(x,y) \\ f(x,y+1) - f(x,y)
\end{pmatrix}
$$

In the same way, the second derivative, called "Laplacian" (French: _laplacien_), is defined by:

$$
\Delta f =
\begin{pmatrix}
  f(x+1,y) - 2f(x,y) + f(x-1,y) \\ f(x,y+1) - 2f(x,y) + f(x,y-1)
\end{pmatrix}
$$


## Gradient operators

Gradient operators are very simple methods for detecting edges.
They use the first derivative and can be calculated using a convolution.
Indeed, the first derivative along the $x$ axis of an image $f$ can be written as a convolution product:

$$
f(x+1,y) - f(x,y) = \sum_m \sum_n h_x(m,n) f(x-m,y-n)
$$

where $h_x$ is a convolution kernel such that:

* $h_x(0,0) = -1$,
* $h_x(-1,0) = +1$,
* and $h_x(m,n) = 0$ elsewhere.

Thus, the kernel $h_x$ is:

$$
h_x =
\begin{pmatrix}
  +1 & -1 \\
  0  & 0 \\
\end{pmatrix}
$$

Similarly, the first derivative along the $y$ axis is written as the convolution of $f$ with the kernel $h_y$:

$$
h_y =
\begin{pmatrix}
  +1 & 0 \\
  -1 & 0 \\
\end{pmatrix}
$$

Note that the row of 0 in $h_x$ and the column of 0 in $h_y$ allows having kernels of the same size.
These two kernels are very the very basic gradient operators
and, in practice, variants of them are used.

### Roberts operators

The Roberts operators are along the diagonals [[Roberts 1965](B:detection:Roberts1965)]:

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


### Prewitt operators

Another variant are the Prewitt operators [[Prewitt 1970](B:detection:Prewitt1970)]
which deal with a kernel with an odd size:

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


### Sobel operators

Finally, the Sobel operators [[Sobel 1968](B:detection:Sobel1968)] are a smoothed version of the Prewitt operators.
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

Note that the sum of the elements is zero, as the Roberts and Prewitt operators.

In {numref}`F:detection:sobel-h-v`, one can see that $h_x$ detects horizontal edges.
For example, the top and bottom of the clock are clearly detected.
The top edge is white because it corresponds to an edge from black to white.
On the contrary, the bottom edge is black.
On the other side, $h_y$ detects vertical edges.

```{figure} sobel-h-v.svg
---
width: 600px
name: F:detection:sobel-h-v
---
Horizontal and vertical Sobel operators.
```


### Magnitude and angle

From the operators above, we also define:

* the magnitude of the edge, which can be interpreted as the "fusion" of the horizontal and vertical Sobel operators:

  $$
  M = \sqrt{ (h_x*f)^2 + (h_y*f)^2 }
  $$
  
  In {numref}`F:detection:sobel-magnitude-angle`, all the edges appear with the same color, whatever their orientation.

* the angle of the edge:
  
  $$
  A = \arctan \left( \frac{h_y*f}{h_x*f} \right)
  $$
  
  In {numref}`F:detection:sobel-magnitude-angle`, the color of the edges corresponds to the angle.
  For example, an angle of $0$ is red, and an angle of $\pi/2$ is blue.

```{figure} sobel-magnitude-angle.svg
---
width: 600px
name: F:detection:sobel-magnitude-angle
---
Magnitude and angle of the Sobel operator.
```


### Thresholding

In some cases, it would be useful to detect the most important edges.
To do that, one can threshold the magnitude to keep only the large values of the gradients.
As you can see in {numref}`F:detection:sobel-magnitude-threshold`, the threshold makes the second hand disappear.
Indeed, the magnitude is lower than other parts of the image because the second hand is gray and not black.

```{figure} sobel-magnitude-threshold.svg
---
width: 600px
name: F:detection:sobel-magnitude-threshold
---
Thresholding the magnitude of the Sobel operator makes the second hands disappear!
```


### The impact of noise

Noise in an image essentially brings great variations in brightness between pixels.
Therefore, the gradient operators is based on the derivative are very sensitive to the noise,
as seen in {numref}`F:detection:edges-derivatives-noise`.
Then it may be useful to denoise the image before edge detection.
In figure {numref}`F:detection:edges-sobel-noise`, a small mean filter is used before the Sobel filter:
the result is much cleaner than without the use of the mean filter.

```{figure} edges-derivatives-noise.svg
---
width: 600px
name: F:detection:edges-derivatives-noise
---
Consequence of noise on the brightness profile and its derivatives
(orange: non-noisy profiles, blue: noisy profiles).
```

```{figure} edges-sobel-noise.svg
---
width: 600px
name: F:detection:edges-sobel-noise
---
Left: noisy image. Center: Sobel operator (magnitude). Right: Sobel operator applied on the result of a $3\times3$ mean filter.
```

## Advanced methods

Following the gradient operators, new methods have been proposed to improve edge detection
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
1. apply a Gaussian filter $g$ on the image $f$ to reduce noise (this is similar to a mean filter),
2. compute the Laplacian (second derivative) $\ell$ on the softened image (this is implemented with a convolution),
3. determine the zero crossings of the result.

As $\ell*(g*f) = (\ell*g)*f$, the first two steps are merged into a single convolution by $\ell*g$.
Hence, the filter $\ell*g$ is the second derivative of a Gaussian:

$$
  (\ell*g)(x,y) = - \left[\frac{x^2+y^2-2\sigma^2}{\sigma^4}\right] \exp\left(-\frac{x^2+y^2}{2\sigma^2}\right).
$$

The filter $\ell*g$ is represented {numref}`F:detection:log`.
It is also called "LoG" for Laplacian of Gaussian (no French equivalent) or Mexican hat (for the resemblance to a sombrero).

```{figure} log.svg
---
width: 500px
name: F:detection:log
---
Laplacian of Gaussian (left: as an image, right: profile along an axis).
```

<!-- Le LoG peut être approximé par une différence de deux gaussiennes. -->

The zero-crossings in the image resulting from the LoG convolution are given by searching for changes of sign in the intensity of two pixels.
{numref}`F:detection:marr-hildreth` gives an example.

```{figure} moulinsart-marr-hildreth.svg
---
name: F:detection:marr-hildreth
---
Marr-Hildreth Detector.
Left: original image,
center: result of the LoG filter,
right: detection of the zeros crossings.
```

```{figure} caramba-marr-hildreth.svg
---
width: 3px
name: F:detection:caramba
```


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
   
    ::::{grid} 1 1 1 1
    :gutter: 3

    :::{grid-item-card}
    1. For each pixel $(x,y)$ in $M$:
       1. Choose the direction (vertical, horizontal or one of the two diagonals) the closest to $A(x,y)$
       1. If $M(x,y)$ is lower than one of its neighbors in the chosen direction then cancel the gradient: $M(x,y)=0$
    :::

    ::::

4. The last step consists of thresholding by hysteresis for the bad edges.
   Two thresholds are therefore defined ($T_\text{high} > T_\text{low}$) and the algorithm below is applied:
      
    ::::{grid} 1 1 1 1
    :gutter: 3

    :::{grid-item-card}
    1. For each pixel $(x,y)$ in $M$:
       1. If $M(x,y) > T_\text{high}$                 then $(x,y)$ is an edge
       1. If $T_\text{low} < M(x,y) < T_\text{high}$  then $(x,y)$ is an edge if and only if it is neighbor of an edge pixel 
       1. If $M(x,y) < T_\text{low}$                  then $(x,y)$ is not an edge
    :::

    ::::
   
{numref}`F:detection:canny` gives an example of Canny edge detection.

```{figure} moulinsart-canny.svg
---
width: 500px
name: F:detection:canny
---
Canny Detector.
```


### Comparison

{numref}`F:detection:sobel-marr-hildreth-canny` shows the results of the Sobel, Marr-Hildreth and Canny detectors on an image.

```{figure} sobel-marr-hildreth-canny.svg
---
name: F:detection:sobel-marr-hildreth-canny
---
Comparison of Sobel, Marr-Hildreth and Canny detectors.
```

In {numref}`F:detection:marr-hildreth-canny`, which compares Marr-Hildreth and Canny detectors,
one can see that the edges detected with Canny detector are better localized.

```{figure} marr-hildreth-canny.svg
---
name: F:detection:marr-hildreth-canny
---
Comparison between Marr-Hildreth and Canny detectors (zoom).
The edges are shown in green.
```