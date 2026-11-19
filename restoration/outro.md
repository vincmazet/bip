# Conclusion


Restoration consists of inverting the direct model of the degradation.
There are primarily two types of degradation: noise and filtering,
which are inverted by denoising and deconvolution methods, respectively.

Three elementary denoising methods have been presented, and have to be chosen according to the noise model:
* the mean filter in case of additive white Gaussian noise (the simplest and most common model for noise),
* the median filter in case of salt-and-pepper noise,
* the filtering of certain areas of the spectrum in case of periodic noise.

Many other methods exist, such as regularization (including TV regularization, among others),
wavelet transforms, statistical approaches, non-local means [[Buades et al. 2005](#B:segmentation:Buades2005)],
and deep learning methods.
While these methods are more complex than the standard approaches detailed in this chapter, they can be far more efficient.

Besides, deconvolution consists of inverting the (generally low-pass) filtering of an observed image.
The inverse filter generally fails because it amplifies the noise present in the image.
The Wiener filter remains the simplest deconvolution method and can give an acceptable result.
More advanced methods have also been developed, such as the Richardson-Lucy algorithm
[[Richardson 1972](#B:segmentation:Richardson1972), [Lucy 1974](#B:segmentation:Lucy1974)]
and Bayesian methods.

<!-- MAP Contrained least squares -->


:::{seealso} References
   
* (B:restoration:Buades2005)=
  A. Buades, B. Coll, J.-M. Morel,
  "A non-local algorithm for image denoising",
  CVPR, 2005.

* (B:restoration:Chambolle2004)=
  A. Chambolle,
  "An Algorithm for Total Variation Minimization and Applications",
  _Journal of Mathematical Imaging and Vision_,
  vol. 20, p. 89--97, 2004.
   
* (B:restoration:Lucy1974)=
  L.B. Lucy,
  "An iterative technique for the rectification of observed distributions",
  _Astronomical Journal_, vol. 79, no 6, p. 745--754, 1974.
   
* (B:restoration:Richardson1972)=
  W.H. Richardson,
  "Bayesian-based iterative method of image restoration",
  _Journal of the Optical Society of America_, vol. 62, no 1, p. 55--59, 1972.

* (B:restoration:Rudin1992)=
   L.I. Rudin, S. Osher, E. Fatemi,
   "Nonlinear total variation based noise removal algorithms",
   _Physica D_,
   vol. 60, no. 1--4, p. 259--268, 1992.

:::