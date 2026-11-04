# Conclusion

In this chapter, we have seen three methods for calculating the intensity of pixels that appear in an image following a modification of the image's geometry.
Without any information on the non-existent pixels, it is necessary to define a model that provides the missing information.

Nearest neighbor interpolation assigns the intensity of a pixel to the same intensity as the nearest pixel.
Bilinear interpolation assigns to the new pixel the value of a surface that passes through the four nearest neighbors of the pixel and that is linear in both dimensions.
Bicubic interpolation does the same but uses more neighbors, thus making it possible to consider that the surface is a cubic polynomial in both dimensions.

<!-- :::{seealso} References

* (B:binary:Bloch2005)=
  I. Bloch *et al.*,
  *Le traitement des images*
  ([volume 1](https://perso.telecom-paristech.fr/bloch/ANIM/poly-anim-t1.pdf),
  [volume 2](https://perso.telecom-paristech.fr/bloch/ANIM/poly-anim-t2.pdf)),
  Polycopié du cours ANIM, Télécom-Paris, 2005.

::: -->