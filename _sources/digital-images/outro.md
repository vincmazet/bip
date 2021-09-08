# Conclusion

A digital image associates at each coordinate $(m,\,n,\,\dots) \in \mathbb{N}^d$ a set of intensity $\{i_1,\dots,i_B\} \in \mathbb{R}^B$.
Generally, images are bidimensional ($d=2$) and either grayscale ($B=1$) or RGB ($B=3$).
To display an image, a colormap must be defined in order to associate a gray level or a color to each intensity.
Some colormaps are very interesting because of their ability to enhance some details in the image.

We have also seen a first tool in image processing, namely the histogram:
it is a representation of the pixel number in function of their intensity.
As with colormaps, histogram transformations change the intensities and are used to enhance details.
Besides, the histogram will be used especially for [Segmentation](C:segmentation:intro).

<!-- Train yourself with this 🎓 [quizz](https://moodle.unistra.fr/mod/quiz/view.php?id=301557) (Moodle only)! -->