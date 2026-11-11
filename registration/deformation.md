(P:registration:deformation)=
# Deformation model


The deformation applied to the source image is a mathematical transformation that can be either linear or non-linear.

A linear transformation is expressed as:
$$
  p' = M p
$$
where
* $p = \begin{pmatrix} x \; y \; 1 \end{pmatrix}^T$ contains the coordinates of pixel $(x,y)$ from the source image,
* $p' = \begin{pmatrix} x' \; y' \; 1 \end{pmatrix}^T$ contains the coordinates of pixel $(x',y')$ from the transformed image,
* $M \in \mathbb{R}^{3\times3}$ is the transformation matrix.

For example, a translation is given by a transformation matrix defined as:
$$
  M = \begin{pmatrix}
    1 & 0 & t_x \\
    0 & 1 & t_y \\
    0 & 0 & 1
  \end{pmatrix}
  \qquad\Rightarrow\qquad
  p' = \begin{pmatrix}
    x' \\
    y' \\
    1
  \end{pmatrix}
  = \begin{pmatrix}
    x + t_x \\
    y + t_y \\
    1
  \end{pmatrix}
$$
The coordinates of pixel $p'$ in the transformed image
correspond to those of pixel $p$ in the source image
after a translation of $t_x$ pixels in $x$ and $t_y$ pixels in $y$.

The transformation change the geometry of the image and the intensities of the transformed image are computed by using @P:interpolation:intro.

:::{note}
Note that defining $p'$ based on $p$ can result in a transformed image containing empty pixels
if no pixel $p$ from the original image $f$ maps to a pixel $p'$ in the transformed image $f'$.
To avoid this and ensure that a value is obtained for every pixel $p'$,
the *inverse* transformation is applied to find the corresponding coordinate (often a non-integer value) in the original image $f$.
Interpolation is then used to determine the value at this coordinate and, consequently, the value of the pixel $p'$.
:::

The next sections illustrate several common transformations.
As an example, @F:registration:transformation:original presents the source image to which the transformation models are applied.

:::{figure} figs/daisy-original.png
:width: 220px
:name: F:registration:transformation:original
The source image.
:::

<!------------------------------------------------------------------------------------------------>

## Euclidean transformation

An Euclidean transformation, also called rigid transformation, is a linear transformation
consisting of a rotation by an angle $\alpha$ and a translation in the two axes of $(t_x,t_y)$.
Thus it is defined by 3 parameters $\theta=\{\alpha,t_x,t_y\}$ and the transformation matrix is:
$$
  M = \begin{pmatrix}
    \cos\alpha & \sin\alpha & t_x \\
    -\sin\alpha & \cos\alpha & t_y \\
    0 & 0 & 1
  \end{pmatrix}
$$

Specifically, a translation is possible if $\alpha=0$,
and a rotation is possible if $(t_x,t_y) = (0,0)$.

:::::{grid} 1 1 3 3
::::{grid-item}
:::{figure} figs/daisy-translation.png
:width: 220px
:name: F:registration:transformation:translation
Translation $(t_x,t_y)=(25, 100)$.
:::
::::

::::{grid-item}
:::{figure} figs/daisy-rotation.png
:width: 220px
:name: F:registration:transformation:rotation
Rotation $\alpha=\pi/6$ (the rotation center is pixel $(0,0)$).
:::
::::

::::{grid-item}
:::{figure} figs/daisy-euclidean.png
:width: 220px
:name: F:registration:transformation:euclidean
Euclidean transformation with $\alpha = \pi/4$ and $(t_x,t_y)=(250,50)$.
:::
::::
:::::

<!------------------------------------------------------------------------------------------------>

## Affine transformation

An affine deformation is defined by 6 parameters: $\theta=\{m_{11}, m_{12}, m_{13}, m_{21}, m_{22}, m_{23}\}$.
It transforms the source image through a combination of translation, rotation, scaling, and shearing.
Parallel lines remain parallel after the deformation, but their angles change.
The deformation matrix is ​​written as:
$$
  M = \begin{pmatrix}
    m_{11} & m_{12} & m_{13} \\
    m_{21} & m_{22} & m_{23} \\
    0 & 0 & 1
  \end{pmatrix}
$$

:::::{grid} 1 1 3 3
::::{grid-item}
:::{figure} figs/daisy-scale.png
:width: 220px
:name: F:registration:transformation:scale
Scale of 0.7.
:::
::::

::::{grid-item}
:::{figure} figs/daisy-shear.png
:width: 220px
:name: F:registration:transformation:shear
Shear of 0.5
:::
::::

::::{grid-item}
:::{figure} figs/daisy-affine.png
:width: 220px
:name: F:registration:transformation:affine
Affine transformation with scale 0.7 and shear 0.5.
:::
::::
:::::

<!------------------------------------------------------------------------------------------------>

## Projective transformation

A projective transformation, also called homography, preserves lines but not necessarily parallelism.
It has 9 parameters which are the 9 elements of the matrix $M$:
$$
  M = \begin{pmatrix}
    m_{11} & m_{12} & m_{13} \\
    m_{21} & m_{22} & m_{23} \\
    m_{31} & m_{32} & m_{33}
  \end{pmatrix}
$$

:::{figure} figs/daisy-projective.png
:width: 220px
:name: F:registration:transformation:projective
Projective transformation with matrix<br />
$
M = \begin{pmatrix}
  0.35   & -0.50  & 245 \\
  0.2    &  0.04  &  57 \\
  0.0004 & -0.002 &   1 \\
\end{pmatrix}
$.
:::


<!------------------------------------------------------------------------------------------------>

## Non-linear transformation

Alternatively, non-linear deformations can be defined using
specific 2D functions (such as polynomials, sinusoids, splines, or wavelets)
or non-parametric deformation fields.

:::{figure} figs/daisy-non-linear.png
:width: 220px
:name: F:registration:transformation:non-linear
Example of non-linear deformation.
:::