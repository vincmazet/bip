(P:interpolation:order3)=
# Bicubic Interpolation

Besides the poor behavior to interpolate high frequencies,
linear interpolation has another significant disadvantage:
the interpolated curve is not continuous in its first derivative at the grid points.
Thus, cubic interpolation uses third-order polynomials to get the "continuous" image.

An example of cubic interpolation is given in @F:interpolation:cubic-1d.
Consider the segment of the interpolation between 1 and 2:
this third-order polynomial is computed by using the four circled points.
Therefore, the whole interpolated function is a piecewise cubic function.

:::{figure} figs/interp-cubic-1d.svg
:width: 100%
:name: F:interpolation:cubic-1d
Cubic interpolation on a 1D example.
Blue and red dots represent the input and output image pixels, respectively.
The purple line is the continuous data reconstructed from the input pixels.
:::

As with previous interpolation methods, the 2D interpolation is made with 1D interpolations on the rows of the image, then on the columns.

An example of bicubic interpolation is given in @F:interpolation:linear-image.

:::{figure} figs/interp-bicubic-2d.svg
:width: 100%
:name: F:interpolation:cubic-image
Example of bicubic interpolation with a scaling of factor of 3.
From left to right:
original 5×5 image (input data),
continuous data,
interpolated 15×15 image (output data).
:::
 
 
<!-- Ideal interpolation / sinc

The ideal interpolation function in Eq. (10.34) is separable. Therefore,
interpolation can as easily be formulated for higher-dimensional images.
We can expect that all solutions to the interpolation problem will also
be separable. Consequently, we need only discuss the 1-D interpolation
problem. Once it is solved, we also have a solution for the n-dimensional
interpolation problem.

Interpolation reduces to a simple operation in the Fourier domain.
As shown by Eq. (10.36), the transfer function of an ideal interpolation kernel is a rectangular (box) function
which is zero outside the wave numbers that can be represented.
This basic fact suggests the following interpolation procedure in Fourier space:

1. Enlarge the matrix of the Fourier transformed image.
   If an $M \times M$ matrix is increased to an $M' \times M'$ matrix,
   the image in the spatial domain is also increased to an $M' \times M'$ image.
   Because of the reciprocity of the Fourier transform, the image size remains unchanged.
   Only the spacing between pixels is decreased,
   resulting in a higher spatial resolution.

2. Fill the padded area in the Fourier space with zeroes
   and compute an inverse Fourier transform.

Theoretically, this procedure results in a perfectly interpolated image.
Unfortunately, it has three drawbacks.

1. The Fourier transform of a finite image
   implies a cyclic repetition of the image in the spatial and Fourier domain.
   Thus, the convolution performed by the Fourier transform is cyclic.
   This means that at the edge of the image,
   convolution continues with the image on the opposite side.
   As the real world is not periodic and interpolation masks are large,
   this may lead to significant distortions of the interpolation
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

<!-- ARTIFACTS : aliasing (et donc échantillonnage, th shannon, filtre anti-repliement mais pas le principe de repliement spectral qui serait trop long >> envoyer vers une réf), blurring ?, edge halo ? (https://www.cambridgeincolour.com/tutorials/image-interpolation.htm) -->
 



