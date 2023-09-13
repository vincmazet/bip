(C:digital-images:definition)=
# What is a digital image?

## Definition

```{margin}
In very specific applications, the images may have a non-rectangular geometry.
For example, some sensors have hexagonal pixels.
We will not deal with this kind of image as it is very rare.
```

A digital image can be seen as a function $f$ from $\mathbb{N}^d$ to $\mathbb{R}^B$:
it associates at each discrete coordinate $(m,\,n,\,\dots) \in \mathbb{N}^d$
a finite set of intensities $\{i_1,\dots,i_B\} \in \mathbb{R}^B$:


$$
\begin{aligned}
  f:\qquad\;
  \mathbb{N}^d &\to \mathbb{R}^B \\
  m,n,\dots    &\mapsto f(m,n,\dots) = \{i_1,\dots,i_B\}.
\end{aligned}
$$

A digital image can also be seen as an array of $d$ dimensions whose elements contain $B$ numbers.

* For example, a [grayscale image](https://en.wikipedia.org/wiki/Grayscale)
  corresponds to $d=2$ (the image has two dimensions) and $B=1$
  (there is only one value per location $(m,n)$: the grayscale intensity).

```{margin}
Using the bands red, green, and blue corresponds to the
[RGB color space](https://en.wikipedia.org/wiki/RGB_color_model).
A color space is a mean to model the colors in some standard way.
Other color space for displaying on screens exist, such as
[HSV](https://en.wikipedia.org/wiki/HSL_and_HSV) (hue, saturation, value or intensity).
```

<!-- cf support de CC "Image formation", slide 23 sur HLS -->

* A common color image corresponds to $d=2$ and $B=3$ bands,
  typically red, green, and blue.

* An [MRI image](https://en.wikipedia.org/wiki/Magnetic_resonance_imaging)
  corresponds to $d=3$ (the image is three-dimensional) and $B=1$.

In the general case of a 2-dimensional image $f(m,n)$ of size $M \times N$,
one uses the coordinate system showed {numref}`F:intro:coordinates`:
the pixel at coordinates $(0,0)$ is on the top left corner of the image.

```{figure} coordinates.png
---
scale: 100%
name: F:intro:coordinates
---
Coordinate system generally used in image processing.

```

## Diversity of images

Digital images can be categorized in various ways.

### Dimension number $d$

Common images, such as photographs, are 2D (2-dimensional) images while other images lie in more than two dimensions.
A 3D image, as seen in MRI scans, is often referred to as a "3D image" or "cube".
A 1D image is essentially a signal.
The elements constituting a 2D image are called _pixels_ ("picture element"),
and those constituting a 3D image are called _voxels_ ("volume element").

### Dimension heterogeneity

In common 2D images, the two dimensions are spatial dimensions.
However, the dimensions can represent another physical domain and be different.
For instance, a video can be seen as a 2D+$t$ image (two spatial dimensions, one temporal dimension);
a functional MRI sequence can be seen as a 3D+$t$ image (three spatial dimensions, one temporal dimension);
and a [hyperspectral image](https://en.wikipedia.org/wiki/Hyperspectral_imaging)
is a 2D+$\lambda$ image (two spatial dimensions, plus a third dimension depending on the wavelength).

### Element dimension $B$

Each element within an image can be scalar or vector.
For instance, pixels in a 2D grayscale image gather only one value: the gray intensity.
Pixels in photography gather three values (the intensity of red, green and blue).
Images from the [Pléiades constellation](https://en.wikipedia.org/wiki/Pleiades_(satellite)) are RVB--IR: they gather four values (red, green, blue, and infrared).

### Element intensity set

Common images have pixel intensities within the range $\{0,1,\dots,255\}$,
but binary images have values in $\{0,1\}$.
Most of the time, the intensities are assumed to be real numbers.