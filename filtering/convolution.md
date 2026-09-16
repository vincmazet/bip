(P:filtering:convolution)=
# Convolution

<!------------------------------------------------------------------------------------------------>

## Definition

Many image processing results come from a modification of one pixel with respect to its neighbors.
This is the case, for example, for blurring.

When this modification is similar in the entire image $g$,
it can be mathematically defined using a second image $h$ which defines the neighbor relationships.
This results in a third image $f$.
This is the so-called convolution [[Jähne 2005, section 4]](B:filtering:Jahne2005) and it is denoted with $*$:

$$
  f(x,y) = (g*h)(x,y) = \sum_m \sum_n g(x-m,y-n) \ h(m,n)
$$

Intuitively, the convolution "spreads" each pixel $(m,n)$ in $g$ following $h$ and proportionally to the intensity $g(m,n)$.
{numref}`F:convolution:sketch` gives an example of the computing of a particular pixel.

:::{figure} figs/convolution.svg
:name: F:convolution:sketch
Example for computing the pixel (1,1) of $f$.
Note that the pixel (0,0) in the PSF is the one at the center.
:::

For the sake of simplicity, the image $h$ is often:
* of odd size ($3\times3$, $5\times5$, $7\times7$...);
* centered, *i.e.* the pixel with coordinates $(0,0)$ is at the center of the image $h$.

The image $h$ is called by different names, depending on the context:
*filter*, *mask*, *kernel*, *window*, *pattern* or *point spread function* (PSF).

Some convolution examples are shown above.

:::::{tab-set}

::::{tab-item} Example 1
:::{figure} figs/conv-example1.svg
:name: F:convolution:example1
The image to the left is the convolution of the other two images.
:::
Since $h$ has only three non-zero pixels, then the convolution formula has only three non-zero terms, and reads:
$$
  f(x,y)
  &= g(x,y) \ h(0,0) + g(x,y-1) \ h(0,1) + g(x,y-2) \ h(0,2) \\
  &= g(x,y) \times 1 + g(x,y-1) \times 2 + g(x,y-2) \times 3.
$$
Then:
$$
  f(1,1) &= g(1,1) \times 1 + g(1,0) \times 2 + g(1,1) \times 3 = g(1,1), \\
  f(1,2) &= g(1,2) \times 1 + g(1,1) \times 2 + g(1,2) \times 3 = g(1,1) \times 2, \\
  f(1,3) &= g(1,3) \times 1 + g(1,2) \times 2 + g(1,3) \times 3 = g(1,1) \times 3.
$$
::::

::::{tab-item} Example 2
:::{figure} figs/conv-example2.svg
:name: F:convolution:example2
The image to the left is the convolution of the other two images.
:::
Another example which is simple enough to verify by calculating the convolution formula by hand.
::::

::::{tab-item} Example 3
:::{figure} figs/conv-example3.svg
:name: F:convolution:example3
The image to the left is the convolution of the other two images.
:::
$g$ is an image composed of only four non-zero pixels.
$h$ is a blurry spot.
The convolution of $g$ by $h$ clearly shows the "spreading" effect:
the result $f$ corresponds to each of the four pixels of $g$,
at the same position as on $g$,
spreading according to the pattern shown on $h$.
Notice that the "spreading" of the two nearby pixels adds up, thus giving a very bright area.
::::

::::{tab-item} Example 4
:::{figure} figs/conv-example4.svg
:name: F:convolution:example4
The image to the left is the convolution of the other two images.
:::
Here, each pixel of $g$ appears twice in $f$:
the result $g$ then becomes the image $f$ which also appears twice.
Another interpretation can be done:
the result corresponds to the two unique pixels of $h$ which spread while reproducing the pattern $g$.
::::

::::{tab-item} Example 5
:::{figure} figs/conv-example5.svg
:name: F:convolution:example5
The image to the left is the convolution of the other two images.
:::
$g$ is an image made up of pixels of different intensities.
Each of these pixels spreads over the result $f$ following the pattern $f$.
This results in a blurry image.
We will see in @P:filtering:filtering that we have applied here a low pass filter on the image $g$.
::::

:::::

<!------------------------------------------------------------------------------------------------>

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


<!------------------------------------------------------------------------------------------------>

(C:convolution-boundaries)=
## Boundaries effects

The convolution formula is not defined on the boundaries of the image:
as an example, computing $f_{1,1}$ in @F:convolution:sketch requires the value of $g_{0,0}$ which is not defined.

Therefore, one has to make assumptions about the pixel values outside the image.
@F:convolution:boundaries-hypotheses shows an image with some possibilities to consider the external pixels,
and @F:convolution:boundaries-results shows the convolution of these images by a Gaussian.

:::{figure} figs/boundaries-hypotheses.svg
:name: F:convolution:boundaries-hypotheses
Several ways to assume the pixels outside the image.
The image is delimited by the green edge.
:::

:::{figure} figs/boundaries-results.svg
:name: F:convolution:boundaries-results
Results of the convolution with the same image.
:::

One can see on the @F:convolution:boundaries-results that the three convolutions are basically identical:
only the pixels near the boundaries may be different (darker or brighter on this example).
Anyway, there is no perfect choice to set the pixels outside the image, and each choice yields some errors.
Also, the best thing is to ensure when acquiring the image that the objects of interest are far from the edges

At last, note that the wrapping hypothesis yields a *circular convolution*.
This is also the result given by a multiplication in the Fourier domain (see @P:filtering:fourier).

<!------------------------------------------------------------------------------------------------>

(P:convolution:separability)=
## Separable Convolution

A separable convolution is when the convolution kernel $h$ can be written as the convolution of two 1D filters
(say $h_1$ and $h_2$) defined along the two axes.
Let's give an example.

If the PSF $h$ can reads

$$
h = \begin{bmatrix}
    \alpha a & \alpha b & \alpha c \\
    \beta  a & \beta  b & \beta  c \\
    \gamma a & \gamma b & \gamma c \\
\end{bmatrix}
$$

then

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


:::{dropdown} Proof

Consider two images $g$ and $h$ of size $M \times N$.

* On the one side, the computation of one pixel by using the 2D convolution
  needs $MN$ multiplications and $MN-1$ additions.
  Therefore, computing the convoluted image needs $(MN+MN-1) \times MN$ operations.

* On the other side, each element of a 1D convolution along one column needs $M$ multiplications and $M-1$ additions.
  Similarly, each element of a 1D convolution along one row needs $N$ multiplications and $N-1$ additions.
  Therefore, computing the convoluted image needs $2(M+N-1) \times MN$ operations.

It is easy to see that $2(M+N-1) \times MN < (MN+MN-1) \times MN$ operations,
highlighting the efficiency of the separability.

:::