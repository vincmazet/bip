# Conclusion

We have seen in that chapter that methods for finding features are very different and depend on the seeking feature.
* For edges, usual methods are essentially a filtering using the gradient or the Laplacian
  (Roberts or Prewitt filters, Sobel or Canny detectors).
* For corners, the dedicated methods analyze the variation in intensity in the neighbourhood of the pixels (Moravec and Harris detectors).
* For lines and circles, the image is represented in the space of the parameters of the geometric shape (Hough transform).

<!-- Parler aussi de classification (dont réseaux de neurones), qui sont utilisées sur des features -->

<!-- Rajouter ? SIFT, SURF, sur images binaires (cf binary.ipynb, ACP, isomap, analyse discriminante sur une image, HoG, descripteurs de Fourier -->
