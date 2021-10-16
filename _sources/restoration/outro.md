# Conclusion


We have seen that there are different types of noise,
the most common model (because the simplest) being additive white Gaussian noise.

Three simple denoising methods have been presented, and have to be chosen depending on the noise model:
* the mean filter in the case of additive white Gaussian noise,
* the median filter in the case of salt-and-pepper noise,
* the filtering of certain areas of the spectrum in the case of periodic noise.

Many other methods exist, for example, regularization (we have seen the TV regularization, but others are possible),
wavelet approaches, statistical approaches, non-local means [Buades et al. 2005]
or deep learning methods.
These methods are more complex than the usual denoising approach detailed in this chapter but are more efficient.

Besides, deconvolution consists of inverting the (generally low-pass) filtering of an observed image.
The inverse filter generally does not work because it tends to increase the noise present in the image.
Wiener filter remains the simplest deconvolution method and can give an acceptable result.
Many other methods have been developed, such as the Richardson-Lucy algorithm [Richardson 1972, Lucy 1974] or Bayesian methods.

<!-- MAP Contrained least squares -->