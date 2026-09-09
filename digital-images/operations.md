(P:digital-images:operations)=
# Arithmetic operations

In the end, an image is an array of numbers.
So mathematical operations can be performed on these numbers.
In this section, we consider 2D images but the generalization to different dimensions is obvious.

<!------------------------------------------------------------------------------------------------>

## Addition

The addition of two images $f$ and $g$ of the same size results in a new image $h$ of the same size
whose pixels are the sum of the pixels in the original images:

$$
\forall m, n,\quad
h(m,n) = f(m,n) + g(m,n).
$$

@F:intro:addition gives an example of image addition to produce an artistic effect.
Addition can also be used to [denoise a series of images](#P:denoising).

:::{figure} figs/addition.svg
:name: F:intro:addition
The image on the right is the sum of the two images on the left.
:::

<!------------------------------------------------------------------------------------------------>

## Subtraction

The subtraction of two images is used for example to detect changes (@F:intro:subtraction).

$$
&\forall m, n,\quad h(m,n) = f(m,n) - g(m,n) \\
\text{or}\qquad
&\forall m, n,\quad h(m,n) = | f(m,n) - g(m,n) |
$$

:::{figure} figs/subtraction.svg
:name: F:intro:subtraction
The image on the right is the difference between the two images on the left.
Note that the image of difference has values between $-255$ and $255$.
:::

<!------------------------------------------------------------------------------------------------>

## Division

The division of two images is used to correct non-homogeneous illumination.
@F:intro:division illustrates the removal of shadow.

$$
\forall m, n,\quad
h(m,n) = \frac{f(m,n)}{g(m,n)}.
$$

:::{figure} figs/division.svg
:name: F:intro:division
The right image is the division of the left image by the right image.
:::