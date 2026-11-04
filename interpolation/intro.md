# Interpolation

<!-- L'interpolation d'une image est le fait de calculer les intensités de nouveaux pixels qui n'existaient pas dans l'image initiale mais qui apparaissent suite à un rééchantillonnage de l'image. Ce rééchantillonnage apparaît par exemple lors du redimensionnement d'une image (cas d'un zoom), au moment de la rotation d'une image ou dans tous les cas où la géométrie de l'image est modifiée. L'idée est de choisir une fonction qui modélise l'évolution spatiale des intensités des pixels et de régler ses paramètres grâce aux intensités des pixels existants. Les intensités des nouveaux pixels sont alors les valeurs de la fonction à l'endroit où se trouvent ces pixels. Dans ce chapitre, nous allons étudier les méthodes d'interpolation les plus courantes : plus proche voisin, bilinéaire, polynomiale, [bicubique]. -->

Image interpolation is a tool used extensively when an image is mapped into a predefined geometry,
by using transformations such as rescaling, translating, shrinking or rotating.
Applications arise in many domains:
creating panoramas in photography, returning a cartographic reference in remote sensing,
or aligning images on anatomical references in medical imaging.

The consequence of a geometric transformation on an image
is that the coordinates of the pixels in the input and the output image no longer coincide.
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

In the next section are listed the three main interpolation methods:
nearest neighbour interpolation (order 0),
bilinear interpolation (order 1),
and bicubic Interpolation (order 3).
In these methods, the "continuous" image is built from a polynomial model.
The order of the polynomial differs between the interpolation methods.