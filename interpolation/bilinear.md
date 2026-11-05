(P:interpolation:order1)=
# Bilinear interpolation

With linear interpolation (French: *interpolation linéaire*),
the interpolated points lie on pieces of straight lines connecting neighbouring grid points.
Because images are in 2D, this method is called *bi*linear interpolation.
This generally gives better results than nearest neighbour interpolation, but structures with high frequencies are not correctly interpolated.

The interpolation relies on one-order polynomials (i.e., linear functions).
The continuous data is modeled as a set of linear functions connecting two pixel intensities.
The intensity of a pixel in the output image is assigned to the value of the linear function at the pixel position.

@F:interpolation:linear-1d illustrates a 1D example of linear interpolation.
The bold segment of the continuous function is determined from two circled data points.

:::{figure} figs/interp-linear-1d.svg
:width: 100%
:name: F:interpolation:linear-1d
Illustration of the linear interpolation on a 1D example.
Blue and red dots represent the input and output image pixels, respectively.
The purple line is the continuous data reconstructed from the input pixels.
:::

The result of bilinear interpolation on an image is given in @F:interpolation:linear-image.

:::{figure} figs/interp-bilinear-2d.svg
:width: 100%
:name: F:interpolation:linear-image
Example of bilinear interpolation with a scaling of factor of 3.
From left to right:
original 5×5 image (input data),
continuous data,
interpolated 15×15 image (output data).
:::