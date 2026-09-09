# Conclusion


We have seen that there are different types of noise,
the most common model (because the simplest) being additive white Gaussian noise.

Three simple denoising methods have been presented, and have to be chosen depending on the noise model:
* the mean filter in the case of additive white Gaussian noise,
* the median filter in the case of salt-and-pepper noise,
* the filtering of certain areas of the spectrum in the case of periodic noise.

Many other methods exist, for example, regularization (we have seen TV regularization, but others are possible),
wavelet approaches, statistical approaches, non-local means [[Buades et al. 2005](B:segmentation:Buades2005)]
or deep learning methods.
These methods are more complex than the usual denoising approach detailed in this chapter but are more efficient.

Besides, deconvolution consists of inverting the (generally low-pass) filtering of an observed image.
The inverse filter generally does not work because it tends to increase the noise present in the image.
Wiener filter remains the simplest deconvolution method and can give an acceptable result.
Many other methods have been developed, such as the Richardson-Lucy algorithm
[[Richardson 1972](B:segmentation:Richardson1972), [Lucy 1974](B:segmentation:Lucy1974)]
or Bayesian methods.

<!-- MAP Contrained least squares -->


## References
   
* (B:segmentation:Buades2005)=
  A. Buades, B. Coll, J.-M. Morel,
  "A non-local algorithm for image denoising",
  CVPR, 2005.

* (B:segmentation:Chambolle2004)=
  A. Chambolle,
  "An Algorithm for Total Variation Minimization and Applications",
  _Journal of Mathematical Imaging and Vision_,
  vol. 20, p. 89--97, 2004.
   
* (B:segmentation:Lucy1974)=
  L.B. Lucy,
  "An iterative technique for the rectification of observed distributions",
  _Astronomical Journal_, vol. 79, no 6, p. 745--754, 1974.
   
* (B:segmentation:Richardson1972)=
  W.H. Richardson,
  "Bayesian-based iterative method of image restoration",
  _Journal of the Optical Society of America_, vol. 62, no 1, p. 55--59, 1972.

* (B:segmentation:Rudin1992)=
   L.I. Rudin, S. Osher, E. Fatemi,
   "Nonlinear total variation based noise removal algorithms",
   _Physica D_,
   vol. 60, no. 1--4, p. 259--268, 1992.
