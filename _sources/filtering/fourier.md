(C:fourier)=
# Fourier transform

The Fourier transform is a very classical tool in image processing.
It is a mathematical transformation that give information about the frequency content of the image.



## Definition

The discrete Fourier transform (DFT) of an image $f$ of size $M \times N$ is an image $F$ of same size computed with the following definition:

$$
  F(u,v) = \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(m,n) e^{-j\,2\pi \left(\frac{um}{M} + \frac{vn}{N}\right)}
$$

In the sequel, we note $\mathcal{F}$ the DFT so that $\mathcal{F}[f] = F$.

Because the DFT of an image is possibly complex, it cannot be displayed with a single image.
That is why we will show the amplitude (modulus) and phase (argument) of the DFT separately, as in {numref}`F:fourier:example`.

```{glue:figure} G:fourier:example
:name: "F:fourier:example"

DFT of the squirrel. The amplitude is shown with a logarithmic scale to distinguish clearly the details (so we have appled an histogram transformation).
```

The amplitude and phase represent the distribution of energy in the frequency plane.
The low frequencies are located in the center of the image, and the high frequencies near the boundaries.
In the figure above, the gray background is a low frequency area because the intensities of the pixels slowly evolve from one pixel to another.
On the contrary, the tail is a high frequency area because the pixel intensity shows a rapid alternation between the hair and the background.

The inverse discrete Fourier transform computes the original image from a Fourier transform:

$$
  f(m,n) = \frac{1}{MN} \sum_{u=0}^{M-1} \sum_{v=0}^{N-1} F(u,v) e^{+j\,2\pi \left(\frac{um}{M} + \frac{vn}{N}\right)}
$$

It is denoted $\mathcal{F}^{-1}$ below.


## Properties

* The DTF is linear:
  
  $$
    \mathcal{F}[af + bg] = aF + bG
    \qquad\text{where}\; a,b\in\mathbb{C}.
  $$
  
* The convolution of two images is equivalent to the multiplication of the DFT of the images:

  $$
    f * g = \mathcal{F}^{-1}[F \times G]
  $$

* Separability: the 2D DFT can be obtained by computing a 1D DFT on the rows, then a 1D DFT on the columns.

* The DTF is periodic with periods $M$ and $N$:
  
  $$
    F(u,v) = F(u+k_mM,v) = F(u,v+k_nN) = F(u+k_mM,v+k_nN)
    \qquad\text{where}\; k_m, k_n \in \mathbb{Z}.
  $$

* A translation on the image implies a phase shift on the DFT:
  
  $$
    \mathcal{F}[f(m-m_0,n-n_0)] = F(u,v) \exp\left(-j2\pi\left(\frac{um_0}{M}+\frac{vn_0}{N}\right)\right)
  $$

* A rotation on the image implies the same rotation on the DFT.
