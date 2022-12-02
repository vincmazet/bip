(labs:lab6)=
# Lab 6


## Denoising

This exercise is intended to evaluate the performances of the denoising method of your choice.
Therefore it is first essential to have an image corrupted by noise and the same image without noise (to compare the denoising method with the actual image).
Then, the denoising method will be evaluated.

### Creation of a noisy image
  
* Recall the mathematical definition of SNR.

* Express the power of the noise in terms of SNR.
  
* In the case of an AWGN,
  the power of the noise is a good estimation of the variance of the Gaussian.
  Express the Gaussian variance $\sigma^2$ in terms of SNR.

* Add noise to the image of your choice then check that the noise level corresponds to the expected SNR.
  For example, noise should be barely visible above 30 dB.
  On the contrary, the image should be difficult to discern below 0 dB.

  ```{note}
  * Be careful to work with `floats`. You may need to convert your image with `.astype(float)`.
  * For convenience, it is recommended to use an image of size less than 1000×1000. Use `skimage.transform.rescale` to reduce the image size.
  * Use a grayscale image (`skimage.color.rgb2gray`).
  * the noise can be created by using `skimage.util.random_noise` with parameter `clip=False` to get a real Gaussian noise.
  ```

### Denoising the noisy image

Now that you dispose of a noisy image and its noiseless version,
you can implement the denoising method you have chosen.

If you choose a mean filter, use `scipy.ndimage.convolve` to filter by a square PSF of size `w` generated as follows:

```
h = np.ones((w,w)) / (w*w)
```

If you choose TV regularization, use `skimage.restoration.denoise_tv_chambolle`.

* Denoise the image with the chosen method.

* Observe visually the effect of the parameter (size of the mean filter or regularization parameter) on the result, especially for extreme values.

* Use `skimage.metrics.mean_squared_error`
  to calculate the mean squared error (MSE, in French EQM for _erreur quadratique moyenne_)
  of the denoised image to have a quantitative measure of the denoising quality.

* Represent the evolution of the MSE according to the parameter, and comment on the result:
  what is the optimal value of this parameter?
  Can you adjust the parameter by knowing the SNR of the image?

* Compare your method with the one implemented by another student.


## Deconvolution

* Load the image [5.1.13](https://sipi.usc.edu/database/database.php?volume=misc&image=18#top).
  It will be called $x$ in the sequel.
<!--   and convert it to floating point numbers with the instruction
  
  ```
  x = x.astype(float)
  ```
  
  where `x` is the image and will be called` x` in the following. -->

* Generate a circular PSF $h$ of radius 10 with `skimage.morphology.disk`.

  ```{margin}
  The inverse filter works not only if the image is not noisy
  but also if the convolution can be equivalent to a multiplication in the Fourier domain.
  The last condition is true if the convolution is circular,
  that is the image $x$ is assumed to be periodic (see [](C:convolution-boundaries)).
  ```
  
* Perform the convolution of $x$ by $h$ to obtain the image $y$.
  To do this, use the function `scipy.ndimage.filters.convolve` with the argument `mode="wrap"` so that the convolution is circular.
  
* Apply the inverse filter on $y$ to get an estimate $\widehat{x} $ of $x$.
  What do you see?

* Add a small noise to the blurred image, then apply the inverse filter again.
  What do you see?

* Now replace the inverse filter with Wiener filter (`skimage.restoration.wiener` with argument `clip=False`).

* Study the influence of the regularization parameter:
  first by observing the result obtained for some values,
  then by representing the evolution of a restoration quality measure (which one?)
  with respect to the values of the regularization parameter.

* What is the optimal value of the regularization parameter?
  Do you agree that it is actually the best value when you look at the estimation?

* Finally, can you conclude on the optimal choice of the regularization parameter, whatever the image?