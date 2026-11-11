# Interpolation

Image interpolation is a tool used extensively when an image is mapped into a predefined geometry,
by using transformations such as rescaling, translating, shrinking or rotating.
Applications arise in many domains:
creating panoramas in photography, returning a cartographic reference in remote sensing,
or aligning images on anatomical references in medical imaging.

<!-- Geometric transformation ? rescale/resize, rotation, translation, stretch, shearing... (cf Jahne fig 10.16 p. 277 + fig 10.15 p. 276)  -->

The consequence of a geometric transformation on an image
is that the coordinates of the pixels in the original (input) and the transformed (output) image no longer coincide.
Thus the pixel intensities in the output image have to be calculated.

:::{figure} figs/interp-grid-image.svg
:width: 400px
:name: F:interpolation:principle
Principle of interpolation.
The blue and red grids schematize the pixels of the input and ouput images, respectively.
The question is: how to compute the intensity of the highlighted pixel of the red grid from the ones of the blue grid?
:::

The basic idea of interpolation is quite simple:
first, reconstruct a "continuous" image from the discrete input image,
then sample this "continuous" image onto the grid of the output image.
Interpolation methods differ in the way the "continuous" image is reconstructed.

In the next section are listed the three main interpolation methods
where the "continuous" image is built from a polynomial model:
* @P:interpolation:order0 (polynomials of order 0),
* @P:interpolation:order1 (polynomials of order 1),
* @P:interpolation:order3 (polynomials of order 3).

As you can see, biquadratic interpolation (polynomials of order 2) is missing.
The reason is that it is never really used in practice.