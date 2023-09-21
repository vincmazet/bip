(filtering:fourier)=
# Fourier transform

The (2D) Fourier transform is a very classical tool in image processing.
It is the extension of the well known [Fourier transform](https://vincmazet.github.io/signal1/fourier/fourier.html)
for signals which decomposes a signal into a sum of complex oscillations (actually, complex exponential).
In image processing, the complex oscillations always come by pair because the pixels have real intensities.

{numref}`F:fourier:decomposition` shows the decomposition of a synthetic image into oscillations.
In this toy-example, the image is simple enough to be decomposed by using only three oscillations.
We will see further that usual images need much more oscillations.
The Fourier transform gives information about the frequency content of the image.

```{figure} fourier-decomposition.svg
---
name: F:fourier:decomposition
---
A synthetic image and the three oscillations (frequencies)
that compose the image.
```


## Direct Fourier transform

The discrete Fourier transform (DFT) of an image $f$ of size $M \times N$ is an image $F$ of same size defined as:

$$
  F(u,v) = \sum_{m=0}^{M-1} \sum_{n=0}^{N-1} f(m,n) e^{-j\,2\pi \left(\frac{um}{M} + \frac{vn}{N}\right)}
$$

In the sequel, we note $\mathcal{F}$ the DFT so that $\mathcal{F}[f] = F$.

Note that the definition of the Fourier transform uses a complex exponential.
In consequence, the DFT of an image is possibly complex, so it cannot be displayed with a single image.
That is why we will show the amplitude (modulus) and phase (argument) of the DFT separately, as in {numref}`F:fourier:example`.

```{figure} fourier-example.svg
---
name: F:fourier:example
---
DFT of the squirrel. The amplitude is shown with a logarithmic scale to distinguish clearly the details
(an [histogram transformation](C:histogram-transformations) has been applied).
```

The amplitude and phase represent the distribution of energy in the frequency plane.
The low frequencies are located in the center of the image, and the high frequencies near the boundaries.

In the figure above, the gray background behind the squirrel is a low frequency area because the intensities of the pixels slowly evolve from one pixel to another.
On the contrary, the tail is a high frequency area because the intensities of the pixels show a rapid alternation between the hair and the background.


## Inverse Fourier transform

The inverse discrete Fourier transform computes the original image from its Fourier transform:

$$
  f(m,n) = \frac{1}{MN} \sum_{u=0}^{M-1} \sum_{v=0}^{N-1} F(u,v) e^{+j\,2\pi \left(\frac{um}{M} + \frac{vn}{N}\right)}
$$

It is denoted $\mathcal{F}^{-1}$ below.


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