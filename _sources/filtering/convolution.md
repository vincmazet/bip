# Convolution


## Definition

Many image processing results come from a modification of one pixel with respect to its neighbors.
When this modification is similar in the entire image $g$,
it can be mathematically defined using a second image $h$ which defines the neighbor relationships.
This results in a third image $f$.
This is the so-called convolution {ref}`[Jahne 2005, section 4] <C:refs>` and it is denoted with $*$:

$$
  f(x,y) = (g*h)(x,y) = \sum_m \sum_n g(x-m,y-n) h(m,n)
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

Some convolution examples are shown in {numref}`F:convolution:example`.

```{glue:figure} G:convolution:example
:name: "F:convolution:example"

Three examples of image convolution.
```


## Properties

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

Therefore, one has to assume some hypotheses of the pixel values oputside the image.
{numref}`F:convolution:boundaries-hypotheses` shows an image with some possibilities to consider the external pixels, and {numref}`F:convolution:boundaries-results` shows the convolution of the former images by a Gaussian.

```{glue:figure} G:convolution:boundaries-hypotheses
:name: "F:convolution:boundaries-hypotheses"

Several ways to set the pixels outside the image.
```

```{glue:figure} G:convolution:boundaries-results
:name: "F:convolution:boundaries-results"

Results of the convolution with the same image.
```

One can see on the {numref}`F:convolution:boundaries-results` that the three convolutions are basically identical:
only the pixels near the boundaries may be different (darker or brighter on this example).
Anyway, there is no perfect choice to set the pixels outside the image, and each choice yields some errors.
Also, the best way is to arrange it so that the objects of interest are far from the edges.

At last, note that the wrapping hypothesis yields a _circular convolution_.
This is also the result given by a multiplication in the Fourier domain (see [](C:fourier)).

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
  
<!--   EVOQUER CONVOLUTION ? -->