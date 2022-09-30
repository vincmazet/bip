(compression:lossy)=
# Lossy compression

## Principle

The most famous lossy compression format for images is JPEG,
created in 1992 by the Joint Photographic Experts Group.
The main idea of JPEG compression is to apply a specific transform to the image
so that most of the coefficients of the transformed image are very small and can be cancelled out,
thus gaining storage at the cost of very little visual degradation.
In addition, this principle is used in lossy compression of audio (MP3) and video (MPEG).

Most of the energy of usual pictures is concentrated in low frequencies,
so the [discrete Fourier transform](filtering:fourier) (DFT) could be a good idea to perform lossy compression.
It appears though that the so-called _discrete cosine transform_ (DCT) is a better choice for computational reasons.
Note that JPEG2000 (which is a newer but rarely used version of JPEG) used a [wavelet transform][C:filtering:wavelets).


## The discrete cosine transform

The DCT of an image $f$ of size $N \times N$ is an image $F$ of same size defined as:

$$
  F(u,v) = \frac{2}{N} C(u) C(v) \sum_{m=0}^{N-1} \sum_{n=0}^{N-1}
  f(m, n) \cos\left[\frac{(2m+1)u\pi}{2N} \right] \cos\left[\frac{(2n+1)v\pi}{2N} \right]
$$

where

$$
  C(u) =
  \begin{cases}
    \frac{1}{\sqrt{2}}  &\text{if}\; u = 0, \\
    1                   &\text{if}\; u > 0.
  \end{cases}
$$

The DCT is similar to [](filtering:fourier) except that the complex exponentials are replaced by cosines.

The DCT decomposes an image into 2D cosines of different frequencies.
Considering an image of size 8 × 8, the 64 possible cosines of the DCT are represented {numref}`F:compression:dct-coefficients`.

```{figure} dct-coefficients.svg
---
name: F:compression:dct-coefficients
---
The 64 coefficients of a DCT of size 8 × 8.
```

## Example of the DCT of an image

To illustrate the DCT applied to an image, consider the image given in {numref}`F:compression:squirrel-crop`,
which is a crop of size 8 × 8 centered on the squirrel snout.

```{figure} squirrel-crop.svg
---
name: "F:compression:squirrel-crop"
---
The 8 × 8 image to be transformed with DCT (right).
```

The 64 coefficients of the DCT of the crop are shown in {numref}`F:compression:squirrel-coefficients`.
As you can see, the coefficient at the top left, which correspond at the lower frequencies
(see {numref}`F:compression:dct-coefficients`) are the largest.

```{figure} squirrel-coefficients.svg
---
name: F:compression:squirrel-coefficients
---
The 64 coefficients of the DCT applied to {numref}`F:compression:squirrel-crop`.
Those which are cancelled are stroked out with a red cross.
```

Because the human eye is less sensitive to high frequencies than low frequencies,
the idea of JPEG compression is to cancel the coefficients at the bottom right in {numref}`F:compression:squirrel-coefficients`.

```{margin}
The expression of the inverse DCT is not given here but is similar to what the inverse Fourier transform is for the Fourier transform.
```

So, we cancel the coefficients stroked with a red cross and reconstruct the image by using the inverse DCT.
The reconstructed image with only 28 coefficients (over 64) is shown in {numref}`F:compression:squirrel-comparison` (right).
As you can see, the result is very similar to the original image, while less than 50 % of the coefficients are kept!
This small example shows the interest of going into the domain of a transformation and canceling certain coefficients.

```{figure} squirrel-comparison.svg
---
name: F:compression:squirrel-comparison
---
The original image (left), the compressed one (middle) and the difference (right, multiplied by 10 to see the differences).
```

## Other steps in JPEG compression

Computing the DCT of the image and using only the low frequency coefficients for reconstruction
is at the heart of JPEG compression.
To gain even more in terms of compression, other steps are added in the actual JPEG compression.
Here are a few.

* Color images are encoded with three channels, the well-known red-green-blue color space.
  [Numerous color spaces](https://en.wikipedia.org/wiki/List_of_color_spaces_and_their_uses) exist aside of the usual RGB one.
  The YCbCr is the one used in JPEG compression
  because the Y channel encodes the brightness of the image and contains important information for the human eye.
  As a result, the other two channels (Cb and Cr) are downsampled to have fewer pixels to store.
  
* The image is divided into 8 × 8 sub-images, and a DCT is computed on each sub-image.

* In the previous section, the high frequency coefficients are canceled.
  In reality, the quantization is done on each coefficient of each DCT,
  but it is finer for low frequency coefficients than for high-frequency ones.

* The array consisting of the 64 coefficients of each sub-image is compressed with a lossless compression method
  ([Huffman coding](https://en.wikipedia.org/wiki/Huffman_coding)).