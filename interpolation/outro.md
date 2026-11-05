# Conclusion

In this chapter, we have seen three methods for calculating the intensity of pixels that appear in an image following a modification of the image's geometry.
Without any information on the non-existent pixels, it is necessary to define a model that provides the missing information.

Nearest neighbour interpolation assigns the intensity of a pixel to the same intensity as the nearest pixel.
Bilinear interpolation assigns to the new pixel the value of a surface that passes through the four nearest neighbors of the pixel and that is linear in both dimensions.
Bicubic interpolation does the same but uses more neighbors, thus making it possible to consider that the surface is a cubic polynomial in both dimensions, yielding a result more natural.
