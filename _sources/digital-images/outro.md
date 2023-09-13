(C:digital-images:outro)=
# Conclusion

A digital image is essentially an array that associates at each coordinate $(m,\,n,\,\dots) \in \mathbb{N}^d$ a set of intensities $\{i_1,\dots,i_B\} \in \mathbb{R}^B$.
Typically, images are two-dimensional ($d=2$) and can be either grayscale ($B=1$) or RGB ($B=3$).
Fundamental image processing operations involve basic array manipulations (addition,subtraction or ddivision).

RGB images reproduces the colors perceived by the human visual system.
This is achieved by employing a red--green--blue Bayer filter during acquisition,
and using red, green, and blue luminophores for display on screen.
This reproduces the three types of cones of the Human eye.

The digitization of a natural image involves both sampling and quantization,
processes that can introduce distortions, such as the moiré effect.
additional distortions that can affect images are noise and blur.

To display an image, a colormap must be defined in order to associate a gray level or a color to each intensity.
Some colormaps are very interesting for their ability to enhance specific image details.


<!-- Train yourself with this 🎓 [quizz](https://moodle.unistra.fr/mod/quiz/view.php?id=301557) (Moodle only)! -->

<!-- Les réfs pour citer les travaux sur lesquels je me base + pour aller plus loin (donner pistes dans ccl) -->

## References

* (B:digital-images:Jahne2005)=
  B. Jähne,
  _Digital Image Processing_,
  Springer, 2005.
