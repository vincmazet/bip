(P:compression:lossy)=
# Lossy compression

<!------------------------------------------------------------------------------------------------>

## Principle

The most famous lossy compression format for images is JPEG,
created in 1992 by the Joint Photographic Experts Group.

The main idea of JPEG compression is to apply a specific transform to the image
so that most of the coefficients of the transformed image are very small and can be canceled out,
thus gaining storage at the cost of very little visual degradation.
This principle is used in lossy compression of audio (MP3) and video (MPEG).

Most of the energy of usual pictures is concentrated in low frequencies,
so the @P:filtering:fourier could be a good idea to perform lossy compression.
It appears though that the so-called *discrete cosine transform* (DCT) is a better choice for computational reasons.
The wavelet transform (WT) is also a good transform and is used in the JPEG2000 format,
which is more recent than JPEG yet rarely used.

<!------------------------------------------------------------------------------------------------>

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

While the DCT resembles to @P:filtering:fourier,
the difference lies in the fact that the DCT decomposes the image into cosines instead of complex exponentials.

The DCT decomposes an image into 2D cosines of different frequencies.
Considering an image of size 8 × 8, the 64 possible cosines of the DCT are represented @F:compression:dct-coefficients.

:::{figure} figs/dct-coefficients.svg
:name: F:compression:dct-coefficients
The 64 coefficients of a DCT of size 8 × 8.
Each coefficient is a 8 × 8 image.
The first coefficient is constant, the other show horizontal and vertical oscillations.
:::

<!------------------------------------------------------------------------------------------------>

## Example of the DCT of an image

To illustrate the DCT applied to an image, consider the image given @F:compression:squirrel-crop,
which is a crop of size 8 × 8 centered on the squirrel's snout.

:::{figure} figs/squirrel-crop.svg
:name: "F:compression:squirrel-crop"
The 8 × 8 image to be transformed with DCT (right).
:::

The 64 coefficients of the DCT of the crop are shown @F:compression:squirrel-coefficients.
As you can see, the coefficients in the top left corner, which correspond to the lower frequencies
(see @F:compression:dct-coefficients) are the largest in magnitude.

:::{figure} figs/squirrel-coefficients.svg
:name: F:compression:squirrel-coefficients
The 64 coefficients of the DCT applied to @F:compression:squirrel-crop.
Those which are cancelled are stroked out with a red cross.
:::

The next step of JPEG compression is the quantization of these coefficients.
Since the human eye is less sensitive to high-frequencies components than low-frequencies components,
the idea of JPEG compression is to quantize roughly the coefficients primarily located in the bottom-right corner of @F:compression:squirrel-coefficients.

To illustrate the process simply, here we cancel the coefficients marked with a red cross and reconstruct the image by using the inverse DCT.
The reconstructed image with only 28 coefficients (over 64) is shown in @F:compression:squirrel-comparison (middle).
As you can see, the result is very similar to the original image (left),
even though less than 50 % of the coefficients are kept!
This small example shows the interest of going into the domain of a transformation
and "canceling" certain coefficients.

:::{margin}
The expression of the inverse DCT is not given here but is similar to what the inverse Fourier transform is for the Fourier transform.
:::

:::{figure} figs/squirrel-comparison.svg
:name: F:compression:squirrel-comparison
The original image (left), the compressed one (middle) and the difference (right, multiplied by 10 to see the differences).
:::

<!------------------------------------------------------------------------------------------------>

## Other steps in JPEG compression

Computing the DCT of the image and using only the low frequency coefficients for reconstruction
is at the heart of JPEG compression.
To gain even more in terms of compression, other steps are added in the actual JPEG compression.
Here are a few.

* Instead of using the [RGB color space](#P:digital-images:rgb-color-model), JPEG compression uses the YCbCr one
  because the Y channel encodes the brightness of the image and contains important information for the human eye.
  As a result, the other two channels (Cb and Cr) are downsampled to have fewer pixels to store.

* In the example given previously, the high frequency coefficients are canceled.
  In reality, the quantization is done on each coefficient of each DCT,
  but it is finer for low-frequency coefficients than for high-frequency ones.

* The array consisting of the 64 coefficients of each sub-image is compressed with a lossless compression method
  ([Huffman coding](https://en.wikipedia.org/wiki/Huffman_coding)).