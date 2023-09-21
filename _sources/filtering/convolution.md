(filtering:convolution)=
# Convolution


## Definition

Many image processing results come from a modification of one pixel with respect to its neighbors.
When this modification is similar in the entire image $g$,
it can be mathematically defined using a second image $h$ which defines the neighbor relationships.
This results in a third image $f$.
This is the so-called convolution [[Jähne 2005, section 4]](B:filtering:Jahne2005) and it is denoted with $*$:

<!-- dire également que ça modélise l'effet d'un instrument de mesure -->

$$
  f(x,y) = (g*h)(x,y) = \sum_m \sum_n g(x-m,y-n) \ h(m,n)
$$

Intuitively, the convolution "spreads" each pixel $(m,n)$ in $g$ following $h$ and proportionally to the intensity $g(m,n)$.
{numref}`F:convolution:sketch` gives an example of the computing of a particular pixel.

```{figure} convolution.png
---
name: F:convolution:sketch
---
Example for computing the pixel (2,2) of $f$.
```

For the sake of simplicity, the image $h$ is often:
* of odd size ($3\times3$, $5\times5$, $7\times7$...);
* centered, _i.e._ the pixel with coordinates $(0,0)$ is at the center of the image $h$.

The image $h$ is called by different names, depending on the context:
_filter_, _mask_, _kernel_, _window_, _pattern_ or _point spread function_ (PSF).

Some convolution examples are shown above.

`````{tab-set}

````{tab-item} Example 1
```{figure} conv-example1.svg
---
name: F:convolution:example1
---
The image to the left is the convolution of the other two images.
```
$g$ is an image composed of only four non-zero pixels.
$h$ is a blurry spot.
The convolution of $g$ by $h$ clearly shows the "spreading" effect:
the result $f$ corresponds to each of the four pixels of $g$,
at the same position as on $g$,
spreading according to the pattern shown on $h$.
Notice that the "spreading" of the two nearby pixels adds up, thus giving a very bright area.
````

````{tab-item} Example 2
```{figure} conv-example2.svg
---
name: F:convolution:example2
---
The image to the left is the convolution of the other two images.
```
$g$ is an image made up of pixels of different intensities.
Each of these pixels spreads over the result $f$ following the pattern $f$.
This results in a blurry image.
We will see in [](filtering:filtering) that we have applied here a low pass filter on the image $g$.
````

````{tab-item} Example 3
```{figure} conv-example3.svg
---
name: F:convolution:example3
---
The image to the left is the convolution of the other two images.
```
Here, each pixel of $g$ appears twice in $f$:
the result $g$ then becomes the image $f$ which also appears twice.
Another interpretation can be done:
the result corresponds to the two unique pixels of $h$ which smear while reproducing the pattern $g$.
````

`````


## Properties

As a mathematical operation, the convolution has several properties.

* The neutral element of convolution is an image filled with zeros but the pixel at the center equals 1.

* The convolution is commutative: &nbsp;
$g*h = h*g$.

* The convolution is distributive with respect to the addition: &nbsp;
$g*(h_1+h_2) = g*h_1 + g*h_2$.

* The convolution is bilinear: &nbsp;
$\alpha (g*h) = (\alpha g) * h = g * (\alpha h)$ &nbsp; (with $\alpha\in\mathbb{C}$).

* The convolution is associative: &nbsp;
$h_1*(h_2*h_3) = (h_1*h_2)*h_3$.



(C:convolution-boundaries)=
## Boundaries effects

The convolution formula is not defined on the boundaries of the image:
as an example, computing $f_{1,1}$ in {numref}`F:convolution:sketch` requires the value of $g_{0,0}$ which is not defined.

Therefore, one has to assume some hypotheses of the pixel values outside the image.
{numref}`F:convolution:boundaries-hypotheses` shows an image with some possibilities to consider the external pixels, and {numref}`F:convolution:boundaries-results` shows the convolution of these images by a Gaussian.

```{figure} boundaries-hypotheses.svg
---
name: F:convolution:boundaries-hypotheses
---
Several ways to assume the pixels outside the image.
The image is delimited by the green edge.
```

```{figure} boundaries-results.svg
---
name: F:convolution:boundaries-results
---
Results of the convolution with the same image.
```

One can see on the {numref}`F:convolution:boundaries-results` that the three convolutions are basically identical:
only the pixels near the boundaries may be different (darker or brighter on this example).
Anyway, there is no perfect choice to set the pixels outside the image, and each choice yields some errors.
Also, the best thing is to ensure when acquiring the image that the objects of interest are far from the edges

At last, note that the wrapping hypothesis yields a _circular convolution_.
This is also the result given by a multiplication in the Fourier domain (see [](filtering:fourier)).

## Separable Convolution

A separable convolution is when the convolution kernel $h$ can be written as the convolution of two 1D filters (say $h_1$ and $h_2$) defined along the two axes.
Let's give an example:

$$
  \underbrace{\begin{bmatrix}
    \alpha a & \alpha b & \alpha c \\
    \beta  a & \beta  b & \beta  c \\
    \gamma a & \gamma b & \gamma c \\
  \end{bmatrix}}_{h}
  =
  \underbrace{\begin{bmatrix}
    0 & \alpha & 0 \\
    0 & \beta & 0 \\
    0 & \gamma & 0 \\
  \end{bmatrix}}_{h_1}
  *
  \underbrace{\begin{bmatrix}
    0 & 0 & 0 \\
    a & b & c \\
    0 & 0 & 0 \\
    \end{bmatrix}}_{h_2}
  =
  \underbrace{\begin{bmatrix}
    \alpha \\
    \beta \\
    \gamma \\
  \end{bmatrix}}_{h_1}
  *
  \underbrace{\begin{bmatrix}
    a & b & c \\
    \end{bmatrix}}_{h_2}
$$

Thus, the convolution of an image $g$ by a separable filter $h$ can be calculated by first computing the convolution of $g$ with $h_1$, then the convolution of the former result with $h_2$ (or the reverse):

$$
  g * h = g * (h_1*h_2) = (g*h_1) * h_2 = (g*h_2) * h_1
$$

The convolution separability saves computation time because the computation of two 1D convolutions requires less operations than the computation of a 2D convolution.

<!-- Exemple pour des images $g$ et $h$ de taille $M \times N$~:

   | multiplications | additions

Sans séparabilité :
  $f(x,y) = \sum_m \sum_n g(x-m,y-n) h(m,n)$ | $MN$      | $MN-1$
  Pour tous les pixels $x,y$~:               | $(MN)^2$  | $MN(MN-1)$

  Avec séparabilité :
  $f_1(x,y) = \sum_m g(x-m,y) h_1(m)$        | $M$       | $M-1$
  $f(x,y) = \sum_n f_1(x,y-n) h_2(n)$        | $N$       | $N-1$
  Pour tous les pixels $x,y$~:               | $MN(M+N)$ | $MN(M+N-2)$ -->


```{dropdown} Proof

Consider two images $g$ and $h$ of size $M \times N$.

* On the one side, the computation of one pixel by using the 2D convolution
  needs $MN$ multiplications and $MN-1$ additions.
  Therefore, computing the convoluted image needs $(MN+MN-1) \times MN$ operations.

* On the other side, each element of a 1D convolution along one column needs $M$ multiplications and $M-1$ additions.
  Similarly, each element of a 1D convolution along one row needs $N$ multiplications and $N-1$ additions.
  Therefore, computing the convoluted image needs $2(M+N-1) \times MN$ operations.

It is easy to see that $2(M+N-1) \times MN < (MN+MN-1) \times MN$ operations,
highlighting the efficiency of the separability.

```