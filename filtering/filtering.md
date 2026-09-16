(P:filtering:filtering)=
# Filtering

The operation of filtering consists of applying a convolution with a specific PSF on an image
so as to modify the image, or to enhance some features, or to reduce some frequencies.

In this section we will see some examples of filters.
First, we begin with common filters (blur, edge detection and sharpening) that are defined from an analysis in the image domain.
Then, we continue with two important families of filters: low-pass and high-pass filters,
which are defined from considerations in the Fourier domain.

<!------------------------------------------------------------------------------------------------>

(P:filtering:blur-filter)=
## Blur filtering

An example of blur filtering is given in @F:blur-filtering.
Each pixel of the output image is a mean of the pixel intensities in a window in the original image.
The PSF in @F:blur-filtering is very simple:

$$
h = \begin{bmatrix}
1 & 1 & 1 & 1 & 1 \\
1 & 1 & 1 & 1 & 1 \\
1 & 1 & 1 & 1 & 1 \\
1 & 1 & 1 & 1 & 1 \\
1 & 1 & 1 & 1 & 1 \\
\end{bmatrix}
$$

:::{figure} figs/blur-filtering.svg
:height: 250px
:name: F:blur-filtering
Blur filtering.
:::

Other size, shape, and coefficients can be used in the PSF as long as it defines a weighted mean.

<!------------------------------------------------------------------------------------------------>

(P:filtering:edge-filter)=
## Edge detection filtering

Edge detection consists of highlighting the borders of the "objects" in the image.
This corresponds to compute the discrete derivatives of a pixel with its four neighbors,
so that a specific pixel $(x,y)$ in the output image $f$ is defined as ($g$ is the original image):

$$
f(x,y)
&=      g(x,y) - g(x-1,y) \\
&+\; g(x,y) - g(x+1,y) \\
&+\; g(x,y) - g(x,y-1) \\
&+\; g(x,y) - g(x,y+1)
$$

so:

$$
f(x,y)= 4g(x,y) - g(x-1,y) - g(x+1,y) - g(x,y-1) - g(x,y+1)
$$

and, through the convolution definition, the PSF is:

$$
h = \begin{bmatrix}
0 & -1 & 0 \\
-1 & 4 & -1 \\
0 & -1 & 0 \\
\end{bmatrix}.
$$

The result is given in @F:edge-filtering.

:::{figure} figs/edge-filtering.svg
:height: 250px
:name: F:edge-filtering
Edge filtering.
:::

<!------------------------------------------------------------------------------------------------>

## Sharp filtering

Sharp filtering strenghtens the border in the image.
Then it can be computed as the sum of the original image with an edge detection.
This yields the following PSF and the output given in @F:sharp-filtering.

$$
h
= \begin{bmatrix}
0 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 0 \\
\end{bmatrix}
+ \begin{bmatrix}
0 & -1 & 0 \\
-1 & 4 & -1 \\
0 & -1 & 0 \\
\end{bmatrix}
= \begin{bmatrix}
0 & -1 & 0 \\
-1 & 5 & -1 \\
0 & -1 & 0 \\
\end{bmatrix}
$$

:::{figure} figs/sharp-filtering.svg
:height: 250px
:name: F:sharp-filtering
Sharp filtering (or sharpening).
:::

<!------------------------------------------------------------------------------------------------>

(P:filtering:lowpass)=
## Low-pass filtering

Because filtering is the convolution of an image with a specific PSF,
it can also be achieved by multiplying the DFT of the image and the DFT of the PSF.
Then it becomes possible to define the filter in the Fourier domain instead of the spatial domain.

@F:lowpass-filtering shows an example of low-pass filtering.
The first row shows the filtering as a convolution in the spatial domain,
the second row shows the same information in the Fourier domain,
where the DFT of the filtered image is the multiplication (point to point) of the DFT of the original image and the PSF.

Low-pass filtering preserves only the low frequencies, yielding a blurred image.

:::{figure} figs/lowpass-filtering.svg
:width: 100%
:name: F:lowpass-filtering
Example of low-pass filtering: only the low frequencies are kept.
Top row: spatial domain, bottom row: amplitude of the DFT
(the phase is not shown for brevity).
:::

Similarly, @P:filtering:blur-filter, as defined above, is also a low-pass filter.

<!------------------------------------------------------------------------------------------------>

## High-pass filtering

Contrary to low-pass filtering, high-pass filtering preserves only the high frequencies,
i.e. the sudden changes in the intensities (@F:highpass-filtering).

:::{figure} figs/highpass-filtering.svg
:width: 100%
:name: F:highpass-filtering
Example of high-pass filtering: only the high frequencies are kept.
Top row: spatial domain, bottom row: amplitude of the DFT
(the phase is not shown for brevity).
:::

Similarly, @P:filtering:edge-filter, as defined above, is also a high-pass filter.


<!------------------------------------------------------------------------------------------------>

## Other filters

It is possible to define filters when only specific frequencies are discarded.
This is useful to remove some unwanted frequencies in the image,
like the ones given by periodic noises (see @P:denoising:periodic-noise-filtering).