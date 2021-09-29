(labs:lab2)=
# Lab 2


## Convolution

The image <a href="../_static/data/smiley.png">smiley.png</a> will be convolved with several PSF.
Before applying the convolutions, you need to convert the image into float (`skimage.img_as_float`)

* What does the acronym PSF stand for?

* Compute the convolution between the image and a Gaussian kernel (`skimage.filters.gaussian`).

* Compute the convolution between the image and the kernel defined by

  $$
    h = \begin{pmatrix} 1 & -1 \end{pmatrix},
  $$
  
  by using `scipy.ndimage.convolve` and initializing $h$ with `numpy.array`.
  
  <!--
    `scipy.ndimage.convolve` est plus adapté que `scipy.signal.convolve2d` pour le traitement d'image.
    En effet, il n'est pas nécessaire de définir l'option 'same' (le résultat a tout de suite la même taille que l'entrée)
    et de plus on peut définir l'hypothèse sur les bords.
   -->
  
* Compute the convolution between the image and a kernel defined by an array of 30 elements equal to 1/30
  (`numpy.ones`).


## Properties of the Fourier transform

* Load the image <a href="../_static/data/s1.png">s1.png</a>
  and compute its discrete Fourier transform (DFT) with `numpy.fft.fft2`.

* Show the DFT of the image with low frequencies at the center (`numpy.fft.fftshift`).
  The magnitude and angle are obtained with `numpy.absolute` and `numpy.angle`.

* Repeat the same operations with images
  <a href="../_static/data/s2.png">s2.png</a>,
  <a href="../_static/data/s3.png">s3.png</a>,
  <a href="../_static/data/s4.png">s4.png</a>, and
  <a href="../_static/data/s5.png">s5.png</a>.
  Analyse the specificities of the images: what can you say about the DFT?


## Filtering aliasing

Aliasing (french: _crénelage_) is a phenomenon that occurs when the image is poorly sampled.
It can be avoided by applying an anti-aliasing filter (french: _filtre anti-repliement_) before sampling.

```{warning}
Do not display the images in the notebook in this exercise!
Jupyter Lab and Matplotlib can create aliasing on display.
Instead, save the images with `skimage.io.imsave` and look at them with an external viewer,
by taking care of using a 100% zoom.
```
  
* Load and display the image <a href="../_static/data/roof.jpg">roof.jpg</a>.
  Then, downsample it (without an anti-aliasing filter) by a factor of three by taking one pixel out of three in the two spatial dimensions,
  which can be done with the instruction
  ```
  f[::3,::3]
  ```
  How does the phenomenon of aliasing appear visually?
  
* Now, apply a Gaussian filter (`skimage.filters.gaussian`) to the original image before downsampling.
  Adjust the filter parameter to minimize aliasing.
  Is the aliasing still visible?
  
* Lastly, replace the Gaussian filter with an ideal low-pass filter,
  which completely eliminates frequencies above the cutoff frequency without modifying the frequencies below.
  The process is:
  1. Compute the DFT of the image,
  2. Define the ideal filter as a zero image with a square of 1 in the Fourier domain,
  3. Multiply the DFT of the image with the filter (this is equivalent to a convolution in the spatial domain),
  4. Compute the inverse DFT of the result (and keep only the real part).
  
  The code below generates a binary square mask of the same size as the image `X`:
  ```{code}
  Mask = np.zeros(X.shape)
  Mask[a:b,c:d] = 1
  ```
  Choose correctly the coordinates `a`, `b`, `c` and `d` to conserve the low frequencies,
  which are located at the center in the DFT (after applying `numpy.fft.fftshift`).
  
  The ideal filter may be defined in the same way as in the exercise [](lab1:synth-image):
  use the function `numpy.zeros` and the indexing `f[m1:m2,n1:n2]=x`.
  Choose the cutoff frequency appropriately to reduce aliasing without altering the image.
  Is the aliasing still visible?
  

## Lossy compression

The heart of JPEG compression is to cancel out weak coefficients of the discrete cosine transform (DCT) of the image.
In this exercise, a simplified version of JPEG compression is implemented
by cancelling the DCT pixels located outside a certain frequency.

* Compute and display the DCT (`scipy.fftpack.dctn` with argument `norm='ortho'`) of the image
  <a href="../_static/data/squirrel.png">squirrel.png</a>.

* Apply a binary mask to the DCT coefficients to cancel the high frequencies.
  Recall that for DCT, the low frequencies are located at the top left corner of the image.

* Display the compressed image using reverse DCT
  (`scipy.fftpack.idctn`, always with the argument `norm='ortho'`).
  What is your opinion about the quality of the compression?
  
* Calculate the mean square error (MSE) defined as:
  
  $$
  MSE = \frac{1}{MN} \sum_ {m,n} (f(m,n) - g(m,n))^2
  $$
  
  where $f$ and $g$ are respectively the images before and after compression, $M$ and $N$ being the dimensions of these images.
  You can use the function `numpy.linalg.norm`.

* Analyze the evolution of the MSE according to the mask size $C$.
  
  
  
<!--
## Magnitude and phase of the Fourier transform

* Load the image [lena.tiff](https://vincmazet.github.io/ftip/_static/data/lena.tiff) and convert it to grayscale.

* Compute its DFT.

* Reconstruct the image by using the inverse DFT, but using a constant magnitude.
  To do that, you have to define the DFT from the magnitude and the argument, considering that
  
  $$
    X = \rho \exp(j\theta)
  $$
  
  where $X$ is the DFT, $\rho$ the magnitude and $\theta$ the phase.
  In Python, the exponential is `numpy.exp` and the multiplication is simply `*`.
  To define a constant magnitude with the same size as the DFT,
  you can use the code:
  
  ```
  numpy.ones(F.shape)
  ```
  
  It is possible that the image is complex, because of numerical errors.
  To avoid this, display the real part (`numpy.real`) of the image.

* Same question, but using the initial magnitude but a constant argument.

* What do you conclude?
-->
  
<!-- 
## convolution et problèmes aux bords

problème aux bords : je donne une image super grande et un filtre.
Je leur demande d'appliquer le filtre sur l'image et de ne sélectionner/afficher qu'une zone (de 100x100).
L'application du filtre sur toute l'image n'est pas possible (image trop grande).
Solution : sélectionner une partie de l'image et y appliquer le filtre.
Mais à cause du bord, il faut sélectionner une image un peu plus grande que ce qui est demandé.
-->

<!--
## convolution et séparabilité
-->

<!--
 ## retrouver le fond dans une vidéo

une séquence de 10 images dans laquelle quelques objets se déplacent
comment retrouver le fond (c'est à dire sans les objets) ?

Idée 1 : division entre images deux à deux pour déterminer quels sont les pixels qui ne changent pas, et les enregistrer comme étant le fond

Idée 2 : filtre médian en chaque pixel
-->