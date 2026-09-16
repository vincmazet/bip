(P:digital-images:outro)=
# Conclusion

A digital image is essentially an array that associates to each coordinate $(m,\,n,\,\dots) \in \mathbb{N}^d$ a set of intensities $\{i_1,\dots,i_B\} \in \mathbb{R}^B$.
Typically, images are two-dimensional ($d=2$) and can be either grayscale ($B=1$) or RGB ($B=3$).

RGB images reproduce the colors perceived by the human visual system.
This is achieved by employing a red--green--blue Bayer filter during acquisition, and using red, green, and blue luminophores for display on a screen.
The digitization of a natural image involves both sampling and quantization, processes that can introduce distortions, such as the moiré effect.
Additional distortions that can affect images are noise and blur.

To display an image, a colormap must be defined in order to associate a gray level or a color to each intensity.
Some colormaps are very interesting for their ability to enhance specific image details.

Fundamental image processing operations involve basic array manipulations (addition, subtraction or division).

The histogram is a graphical representation of the intensity distribution in a digital image:
the horizontal axis represents the intensities and the vertical axis represents the number of pixels at each intensity.
It shows how the intensities of the pixels are distributed, regardless of their spatial position.
The histogram will be used especially for @C:segmentation:intro.

The next chapters list more complex tools for modifying the image or extracting information from it.


:::{seealso} References

* (B:histogram:Gonzalez2010)=
  R.C. Gonzalez and R.E. Woods,
  _Digital Image Processing_,
  Pearson, 2010.

* (B:digital-images:Jahne2005)=
  B. Jähne,
  _Digital Image Processing_,
  Springer, 2005.

:::