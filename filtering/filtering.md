(P:filtering:filtering)=
# Filtering

The operation of filtering consists of applying a convolution with a specific PSF on an image
so as to modify the image, or to enhance some features, or to reduce some frequencies.

In this section we will see some examples of filters.
First, we begin with common filters (blur, edge detection and sharpening) that are defined from an analysis in the image domain.
Then, we continue with two important families of filters: low-pass and high-pass filters,
which are defined from considerations in the Fourier domain.

(P:filtering:blur-filter)=
## Blur filtering

An example of blur filtering is given in {numref}`F:blur-filtering`.
Each pixel of the output image is a mean of the pixel intensities in a window in the original image.
The PSF in {numref}`F:blur-filtering` is very simple:

$$
h = \begin{bmatrix}
1 & 1 & 1 & 1 & 1 \\
1 & 1 & 1 & 1 & 1 \\
1 & 1 & 1 & 1 & 1 \\
1 & 1 & 1 & 1 & 1 \\
1 & 1 & 1 & 1 & 1 \\
\end{bmatrix}
$$

Other size, shape, and coefficients can be used in the PSF as long as it defines a (possibly weighted) mean.

```{figure} blur-filtering.svg
---
height: 200px
name: F:blur-filtering
---
Blur filtering.
```

(C:filtering:edge-filter)=
## Edge detection filtering

Edge detection consists of highlighting the borders of the "objects" in the image.
This corresponds to compute the discrete derivatives of a pixel with its four neighbors,
so that a specific pixel $(x,y)$ in the output image $f$ is defined as ($g$ is the original image):

$$
f(x,y)
&=      g(x,y) - g(x-1,y) \\
&\quad+\; g(x,y) - g(x+1,y) \\
&\quad+\; g(x,y) - g(x,y-1) \\
&\quad+\; g(x,y) - g(x,y+1) \\
&= 4g(x,y) - g(x-1,y) - g(x+1,y) - g(x,y-1) - g(x,y+1) \\
$$

Thus the PSF in this case is:

$$
h = \begin{bmatrix}
0 & -1 & 0 \\
-1 & 4 & -1 \\
0 & -1 & 0 \\
\end{bmatrix}
$$

The result is given in {numref}`F:edge-filtering`.

```{figure} edge-filtering.svg
---
height: 200px
name: F:edge-filtering
---
Edge filtering.
```

## Sharp filtering

Sharp filtering strenghtens the border in the image.
Then it can be computed as the sum of the original image with an edge detection.
This yields the following PSF and the output given in {numref}`F:sharp-filtering`.

$$
h = \begin{bmatrix}
0 & -1 & 0 \\
-1 & 5 & -1 \\
0 & -1 & 0 \\
\end{bmatrix}
$$

```{figure} sharp-filtering.svg
---
height: 200px
name: F:sharp-filtering
---
Sharp filtering (or sharpening).
```

(filtering:lowpass)=
## Low-pass filtering

Because filtering is the convolution of an image with a specific PSF,
it can also be achieved by multiplying the DFT of the image and the DFT of the PSF.
Then it becomes possible to define the filter in the Fourier domain instead of the spatial domain.

{numref}`F:lowpass-filtering` shows an example of low-pass filtering.
The first row shows the filtering as a convolution in the spatial domain,
the second row shows the same information in the Fourier domain,
where the DFT of the filtered image is the multiplication (point to point) of the DFT of the original image and the PSF.

Low-pass filtering preserves only the low frequencies, yielding a blurred image.

```{figure} lowpass-filtering.svg
---
height: 400px
name: F:lowpass-filtering
---
Example of low-pass filtering: only the low frequencies are kept.
Top row: spatial domain, bottom row: amplitude of the DFT
(the phase is not shown for brevity).
```

Similarly, the [blur filter](C:filtering:blur-filter) defined above is also a low-pass filter.

## High-pass filtering

Contrary to low-pass filtering, high-pass filtering preserves only the high frequencies,
i.e. the sudden changes in the intensities ({numref}`F:highpass-filtering`).

```{figure} highpass-filtering.svg
---
height: 400px
name: F:highpass-filtering
---
Example of high-pass filtering: only the high frequencies are kept.
Top row: spatial domain, bottom row: amplitude of the DFT
(the phase is not shown for brevity).
```

Similarly, the [edge detection](C:filtering:edge-filter) filter defined above is also a high-pass filter.

```{margin}
To go further, it is possible to define filters when only specific frequencies are discarded.
This is useful to remove some unwanted frequencies in the image,
like the ones given by periodic noises (see [](C:denoising:periodic-noise-filtering)).
```