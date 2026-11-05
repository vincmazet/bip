(P:interpolation:order0)=
# Nearest neighbour interpolation

Nearest neighbour interpolation (French: *interpolation au plus proche voisin*) is the simplest interpolation method.

The interpolation relies on zero-order polynomials (i.e., constant functions).
The continuous data is modeled as a set of constant functions whose amplitudes are the pixel intensities.
Then, the intensity of a pixel in the output image is assigned to the intensity of the closest pixel in the input image.

@F:interpolation:nearest-1d illustrates a 1D example of nearest neighbour interpolation.
The bold segment of the continuous function is determined solely from the circled data point.

:::{figure} figs/interp-nearest-1d.svg
:width: 100%
:name: F:interpolation:nearest-1d
Illustration of the nearest neighbour interpolation on a 1D example.
Blue and red dots represent the input and output image pixels, respectively.
The purple line is the continuous data reconstructed from the input pixels.
:::

In 2D, a first 1D interpolation is made on each row of the image,
then a second 1D interpolation is made on the columns.
@F:interpolation:nearest-image shows and example of nearest neighbour interpolation.

:::{figure} figs/interp-nearest-2d.svg
:width: 100%
:name: F:interpolation:nearest-image
Example of nearest neighbour interpolation with a scaling of factor of 3.
From left to right:
original 5×5 image (input data),
continuous data,
interpolated 15×15 image (output data).
:::