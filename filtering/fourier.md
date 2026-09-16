(P:filtering:fourier)=
# Fourier transform

The (2D) Fourier transform is a very classical tool in image processing.
It is the extension of the [Fourier transform](https://vincmazet.github.io/signal1/fourier/intro/)
for signals which decomposes a signal into a sum of complex oscillations (actually, complex exponentials).
In image processing, the Fourier transform decomposes an image into a sum of oscillations with different frequencies, phase and orientation.

So, the Fourier transform gives information about the frequency content of the image,
*i.e.* how the intensities in the image are distributed through different frequencies.
@F:fourier:decomposition shows the decomposition of a synthetic image into oscillations.
In this toy-example, the image is simple enough to be decomposed by using only three oscillations.
We will see further that usual images need much more oscillations.

:::{figure} figs/fourier-decomposition.svg
:name: F:fourier:decomposition
A synthetic image and the three oscillations (frequencies)
that compose the image.
The third oscillation (on the right) is of lower frequency than the first two oscillations,
because the alternation of black and white pixel is smoother than on the first oscillations.
:::

<!------------------------------------------------------------------------------------------------>

## Direct Fourier transform

The discrete Fourier transform (DFT) of an image $f$ of size $M \times N$ is an image $F$ of same size defined as:

$$
  F(u,v) = \sum_{m=0}^{M-1} \sum_{n=0}^{N-1} f(m,n) e^{-j\,2\pi \big(um/M + vn/N\big)}
$$

In the sequel, we note $\mathcal{F}$ the DFT so that $\mathcal{F}[f] = F$.

Note that the definition of the Fourier transform uses a complex exponential.
In consequence, the DFT of an image is possibly complex, so it cannot be displayed with a single image.
That is why we will show the amplitude (modulus) and phase (argument) of the DFT separately, as in @F:fourier:example.

:::{figure} figs/fourier-example.svg
:name: F:fourier:example
DFT of the squirrel. The amplitude is shown with a logarithmic scale to distinguish clearly the details
(an [histogram transformation](P:digital-images:histogram:transformations) has been applied).
:::

The amplitude and phase represent the distribution of energy in the frequency plane.
The intensities of the low frequencies are located in the center of the image, and the intensities of the high frequencies near the boundaries.

In the figure above, the gray background behind the squirrel "contains" mainly low frequencies because the intensities of the pixels slowly evolve from one pixel to another.
On the contrary, high frequencies are needed in the tail to show the rapid alternation between the hair and the background.

<!------------------------------------------------------------------------------------------------>

## Inverse Fourier transform

The inverse discrete Fourier transform computes the original image from its Fourier transform:

$$
  f(m,n) = \frac{1}{MN} \sum_{u=0}^{M-1} \sum_{v=0}^{N-1} F(u,v) e^{+j\,2\pi \big(um/M + vn/N\big)}
$$

It is denoted $\mathcal{F}^{-1}$ below.

<!------------------------------------------------------------------------------------------------>

## Example of simple Fourier transforms

In the examples below, the image (and their FFT) are 16×16 grayscale images.

::::{card}
:::{image} figs/fourier-0.svg
:width: 500px
:align: left
:::
On this example, only the pixel at frequency (0,0) in the Fourier domain is non zero.
Because an oscillation with frequency 0 does not oscillate, the image is constant.
::::

::::{card}
:::{image} figs/fourier-1.svg
:width: 500px
:align: left
:::
Two pixels in the Fourier domain are non zero.
Because they are at frequency 1 along the x-axis,
the image is a sinusoid along the x-axis.
::::

::::{card}
:::{image} figs/fourier-2.svg
:width: 500px
:align: left
:::
Same example as above along the y-axis:
the image is then a sinusoid along the y-axis.
::::

::::{card}
:::{image} figs/fourier-3.svg
:width: 500px
:align: left
:::
Same example as above with a change in the phase.
Therefore, the sinusoid is translated in the spatial domain.
::::

::::{card}
:::{image} figs/fourier-4.svg
:width: 500px
:align: left
:::
Here, there is a oscillations both in x and y,
with high frequency in x and low frequency in y.
::::

::::{card}
:::{image} figs/fourier-5.svg
:width: 500px
:align: left
:::
Two waves with are superimposed, both with the same frequency and phase but different orientations and amplitudes.
::::

::::{card}
:::{image} figs/fourier-full.svg
:width: 500px
:align: left
:::
By combining oscillations at appropriate frequencies, phase and amplitudes,
it is possible to generate a specific image
(here, the mean of the image is set to 0).
::::

<!------------------------------------------------------------------------------------------------>

## Properties

* The DFT is linear:
  
  $$
    \mathcal{F}[af + bg] = aF + bG
    \qquad\text{where}\; a,b\in\mathbb{C}.
  $$
  
* The convolution of two images is equivalent to the multiplication of the DFT of the images,
  provided that the convolution is circular (wrapping hypothesis on the edges):

  $$
    f * g = \mathcal{F}^{-1}[F \times G]
  $$

* The DFT is separable: it can be obtained by computing a 1D DFT on the rows, then a 1D DFT on the columns.

* The DFT is periodic with periods $M$ and $N$ ($k, l \in \mathbb{Z}$):
  
  $$
    F(u,v) = F(u+kM,v) = F(u,v+lN) = F(u+kM,v+lN).
  $$

* A translation on the image implies a phase shift on the DFT:
  
  $$
    \mathcal{F}[f(m-m_0,n-n_0)] = F(u,v) \exp\left(-j2\pi\left(\frac{um_0}{M}+\frac{vn_0}{N}\right)\right)
  $$

* A rotation on the image implies the same rotation on the DFT.

<!-- Illustrer toutes ces propriétés -->
