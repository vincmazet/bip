(C:interpolation)=
# Interpolation methods

## Nearest neighbour interpolation (order 0)

Nearest neighbour interpolation (French: _interpolation au plus proche voisin_) is the simplest method.
The intensity of a pixel in the output image is assigned to the intensity of the closest pixel in the input image.

An example of nearest neighbour interpolation in 1D is given in {numref}`F:interpolation:nearest-1d`.

```{figure} interp-nearest-1d.svg
---
width: 400px
name: F:interpolation:nearest-1d
---
Illustration of the nearest neighbour interpolation on a 1D example.
The blue dots represent the input image pixels,
the red dots represent the output image pixels.
The gray line is the continuous image reconstructed from the input image.
```

In 2D, a 1D interpolation is made on each row of the image,
then a last 1D interpolation is made on the column, as illustrated in {numref}`F:interpolation:nearest-3d`.

```{figure} interp-nearest-3d.svg
---
width: 450px
name: F:interpolation:nearest-3d
---
Illustration of the nearest neighbour interpolation on a 2D example:
the interpolation is separated into the two dimensions.
```

The result of nearest-neighbour interpolation on an image is given in {numref}`F:interpolation:nearest-image`.

```{figure} interp-nearest-2d.svg
---
width: 300px
name: F:interpolation:nearest-image
---
Example of nearest-neighbour interpolation of the 4×4 image in {numref}`F:interpolation:nearest-3d`.
The circles shows the 16 pixels of the original image.
```

<!-- ```{figure} interp-0-image.svg
---
width: 450px
name: F:interpolation:nearest-image
---
Example of nearest-neighbour interpolation, with the same grid as in {numref}`F:interpolation:principle`.
The original image is of size 32$\times$32.
(For clarity, the grid depicted in {numref}`F:interpolation:principle` shows squares of size $2\times2$ pixels).
``` -->

(P:interpolation:bilinear)=
## Bilinear interpolation (order 1)

With linear interpolation (French: _interpolation linéaire_),
the interpolated points lie on pieces of straight lines connecting neighbouring grid points.
Because images are in 2D, this method is called <i>bi</i>linear interpolation.
This generally gives better results than nearest neighbour interpolation, but structures with high frequencies are not correctly interpolated.

An example of linear interpolation is given in {numref}`F:interpolation:linear-1d`,
and the principle of bilinear interpolation is shown in {numref}`F:interpolation:linear-3d`.

```{figure} interp-linear-1d.svg
---
width: 450px
name: F:interpolation:linear-1d
---
Linear interpolation on a 1D example.
```

```{figure} interp-linear-3d.svg
---
width: 450px
name: F:interpolation:linear-3d
---
Illustration of bilinear interpolation on a 2D example:
the interpolation is separated into the two dimensions.
```

The result of bilinear interpolation on an image is given in {numref}`F:interpolation:linear-image`.

```{figure} interp-bilinear-2d.svg
---
width: 300px
name: F:interpolation:linear-image
---
Example of bilinear interpolation of the 4×4 image in {numref}`F:interpolation:linear-3d`.
The circles shows the 16 pixels of the original image.
```

<!-- 
```{figure} interp-1-image.svg
---
width: 450px
name: F:interpolation:linear-image
---
Example of bilinear interpolation.
See how much more natural the result is compared to nearest-neighbor interpolation.
``` -->

## Bicubic Interpolation (order 3)

<!-- bicubique = cubic splines ? -->

The principle of linear interpolation was that a straight line was drawn to pass through two neighbouring points.
Besides its poor behavior to interpolate high frequencies,
linear interpolation has another signiﬁcant disadvantage:
the interpolated curve is not continuous in its ﬁrst derivative at the grid points.

Thus, cubic interpolation uses third-order polynomials to get the "continuous" image.
An example of cubic interpolation is given in {numref}`F:interpolation:cubic-1d`.
Consider the part of the interpolation between 1 and 2:
this third-order polynomial is computed by using the four points identified with the arrows.
Therefore, the whole interpolated function is a piecewise cubic function.

```{figure} interp-cubic-1d.svg
---
width: 450px
name: F:interpolation:cubic-1d
---
Cubic interpolation on a 1D example.
```

As with previous interpolation methods, the 2D interpolation is made with 1D interpolation on the rows of the image, then on the columns,
as shown in {numref}`F:interpolation:cubic-3d`.

```{figure} interp-cubic-3d.svg
---
width: 450px
name: F:interpolation:cubic-3d
---
Illustration of the bicubic interpolation on a 2D example:
the interpolation is separated into the two dimensions.
```

Finally, the result of bicubic interpolation on an image is given in {numref}`F:interpolation:linear-image`.

```{figure} interp-bicubic-2d.svg
---
width: 300px
name: F:interpolation:cubic-image
---
Example of bilinear interpolation of the 4×4 image in {numref}`F:interpolation:cubic-3d`.
The circles shows the 16 pixels of the original image.
```

<!-- ```{figure} interp-3-image.svg
---
width: 450px
name: F:interpolation:cubic-image
---
Example of bicubic interpolation.
``` -->
 
 
<!-- ## Ideal interpolation > sinc ?

The ideal interpolation function in Eq. (10.34) is separable. Therefore,
interpolation can as easily be formulated for higher-dimensional images.
We can expect that all solutions to the interpolation problem will also
be separable. Consequently, we need only discuss the 1-D interpolation
problem. Once it is solved, we also have a solution for the n-dimensional
interpolation problem.

Interpolation reduces to a simple operation in the Fourier domain.
As shown by **Eq. (10.36)**, the transfer function of an ideal interpolation kernel is a rectangular (box) function
which is zero outside the wave numbers that can be represented.
This basic fact suggests the following interpolation procedure in Fourier space:

1. Enlarge the matrix of the Fourier transformed image.
   If an $M \times M$ matrix is increased to an $M' \times M'$ matrix,
   the image in the spatial domain is also increased to an $M' \times M'$ image.
   Because of the reciprocity of theInterpolation comes when an image is interpolated

consists of calculating the intensities of new pixels that do not exist in the image but that appear following a resampling of the image. This resampling appears for example when resizing an image (case of a zoom), when rotating an image or in all cases where the geometry of the image is modified. The idea is to choose a function that models the spatial evolution of the intensities of the pixels and to adjust its parameters using the intensities of the existing pixels. The intensities of the new pixels are then the values ​​of the function at the location where these pixels are located. In this chapter, we will study the most common interpolation methods: nearest neighbor, bilinear, polynomial, [bicubic]le -->




<!-- L'interpolation d'une image est le fait de calculer les intensités de nouveaux pixels qui n'existaient pas dans l'image initiale mais qui apparaissent suite à un rééchantillonnage de l'image. Ce rééchantillonnage apparaît par exemple lors du redimensionnement d'une image (cas d'un zoom), au moment de la rotation d'une image ou dans tous les cas où la géométrie de l'image est modifiée. L'idée est de choisir une fonction qui modélise l'évolution spatiale des intensités des pixels et de régler ses paramètres grâce aux intensités des pixels existants. Les intensités des nouveaux pixels sont alors les valeurs de la fonction à l'endroit où se trouvent ces pixels. Dans ce chapitre, nous allons étudier les méthodes d'interpolation les plus courantes : plus proche voisin, bilinéaire, polynomiale, [bicubique]. Fourier transform, the image size remains unchanged.
   Only the spacing between pixels is decreased,
   resulting in a higher spatial resolution.

2. Fill the padded area in the Fourier space with zeroes
   and compute an inverse Fourier transform.

Theoretically, this procedure results in a perfectly interpolated image.
Unfortunately, it has three drawbacks.

1. The Fourier transform of a ﬁnite image
   implies a cyclic repetition of the image in the spatial and Fourier domain.
   Thus, the convolution performed by the Fourier transform is cyclic.
   This means that at the edge of the image,
   convolution continues with the image on the opposite side.
   As the real world is not periodic and interpolation masks are large,
   this may lead to signiﬁcant distortions of the interpolation
   even at quite large distances from the edges of the image.

2. The Fourier transform can be computed eﬃciently
   only for a specified number of values for $M'$.
   Best known are the fast radix-2 algorithms that can be applied
   only to images of the size $M' = 2^{N'}$.
   Therefore, the Fourier transform-based interpolation is slow for numbers $M'$ 
   that cannot be expressed as a product of many small factors.
   
3. As the Fourier transform is a global transform, it can be applied only to scaling.
   According to the generalized similarity theorem,
   it could also be applied to rotation and affine transforms.
   But then the interpolation problem is only shifted
   from the spatial domain to the wave number domain.
 -->

 

<!-- artifacts : aliasing (et donc échantillonnage, th shannon, filtre anti-repliement mais pas le principe de repliement spectral qui serait trop long >> envoyer vers une réf), blurring ?, edge halo ? (https://www.cambridgeincolour.com/tutorials/image-interpolation.htm) -->
 

<!-- then this continuous image is filtered so as to give an image whose spectrum is compatible with the new sampling that we wish t carry out,

The basis of interpolation is the sampling theorem (Section 9.2.2).
This theorem states that the digital image completely represents the
continuous image provided the sampling conditions are met. In short
it means that each periodic structure that occurs in the image must be
sampled at least twice per wavelength.

These resampling operations rely on mathematical bases of the Shannon samling theory.

The fact that interpolation is a convolution operation and thus can
be described by a transfer function in Fourier space Eq. (10.36) gives
us a handy tool to rate the errors associated with an interpolation tech-
nique.

 -->


<!-- Geometric transformation ? rescale/resize, rotation, translation, stretch, shearing... (cf Jahne fig 10.16 p. 277 + fig 10.15 p. 276) -->


