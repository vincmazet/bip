(P:digital-images:definition)=
# What is a digital image?

<!------------------------------------------------------------------------------------------------>

(P:digital-images:definition:definition)=
## Definition

:::{aside}
In very specific applications, the images may have a non-rectangular geometry.
For example, some sensors have hexagonal pixels.
We will not deal with this kind of image as it is very rare.
:::

A digital image is a visual representation of an array of number that represents a physical phenomenon.
It can be seen as a function $f$ from $\mathbb{N}^d$ to $\mathbb{R}^B$:
it associates at each discrete coordinate $(m,\,n,\,\dots) \in \mathbb{N}^d$
a finite set of intensities $\{i_1,\dots,i_B\} \in \mathbb{R}^B$:

$$
\begin{aligned}
  f:\qquad\;
  \mathbb{N}^d &\to \mathbb{R}^B \\
  m,n,\dots    &\mapsto f(m,n,\dots) = \{i_1,\dots,i_B\}.
\end{aligned}
$$

A digital image can also be seen as an array of $d$ dimensions where each element gathers $B$ numbers.
Some examples are now given.

* A grayscale image corresponds to $d=2$ (the image has two dimensions) and $B=1$:
  each element $(m,n)$ corresponds to only one number coding the grayscale intensity.

* A common color image corresponds to $d=2$ and $B=3$ bands,
* the three bands code typically the amount of red, green, and blue.

* An [MRI image](https://en.wikipedia.org/wiki/Magnetic_resonance_imaging)
  corresponds to $d=3$ (the image is three-dimensional) and $B=1$.

In the general case of a 2-dimensional image $f(m,n)$ of size $M \times N$,
one uses the coordinate system showed @F:intro:coordinates:
the pixel at coordinates $(0,0)$ is on the top left corner of the image.

:::{figure} figs/coordinates.png
:scale: 100%
:name: F:intro:coordinates
Coordinate system generally used in image processing.
:::

<!------------------------------------------------------------------------------------------------>

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

Each element within an image can be scalar ($B=1$) or vector ($B>1$).
For instance, pixels in a 2D grayscale image gather only one value: the gray intensity.
Pixels in photography gather three values (the intensity of red, green and blue).
Images from the [Pléiades constellation](https://en.wikipedia.org/wiki/Pleiades_(satellite)) are RVB--IR: they gather four values (red, green, blue, and infrared).

### Element intensity set

Common images have pixel intensities within the range $\{0,1,\dots,255\}$,
but binary images have values in $\{0,1\}$.
Most of the time, the intensities are assumed to be real numbers.

<!------------------------------------------------------------------------------------------------>

## File format

An image file format is a standard way to organize and store image data in a computer file.
Various criteria are taken into account to choose the format adapted to the application.
The list below gives the main characteristics of the most common image file formats.

<!-- Sources
Liste des formats d’image, leurs fonctionnalités et leurs prises en charge par les navigateurs et logiciels de retouche d’image
https://developer.mozilla.org/fr/docs/Web/Media/Guides/Formats/Image_types
-->

:::{dropdown} AVIF
- Name: AV1 Image File Format
- Developed in 2019 by the Alliance for Open Media
- File extenstion: .avif
- Lossless and lossy compression
- Can handle transparency ($B=4$)
- Maximum size: $2^{16} \times 2^{16}$
- 12 bits/band
:::

:::{dropdown} BMP
- Name: BitMaP
- Developed in 1985 by Microsoft
- File extension: .bmp	
- Lossless compression
- Can handle transparency ($B=4$)
- Maximum size: $2^{31} \times 2^{31}$
- 8 bits/band
:::

:::{dropdown} HEIC
- Name: High Efficiency Image Format
- Developed in 2013 by the Video Coding Experts Group
- File extenstion: .heic, .heif
- Lossless and lossy compression
- Can handle transparency ($B=4$)
- Maximum size: $2^{14} \times 2^{14}$
- 10 bits/band
:::

:::{dropdown} GIF
- Name: Graphics Interchange Format
- Developed in 1987 by CompuServe
- File extenstion: .gif	
- No compression
- Can handle transparency ($B=4$), but coded only on 1 bit
- Maximum size: $2^{16} \times 2^{16}$
- 256 colors from a 24-bits RVB colormap
:::

:::{dropdown} JPEG
- Name: Joint Photographic Expert Group
- Developed in 1992 by the Joint Photographic Expert Group
- File extenstion: .jpg, .jpeg
- Lossless and lossy compression
- No transparency ($B=3$)
- Maximum size: $2^{16} \times 2^{16}$
- 8 bits/band
:::

:::{dropdown} JPEG 2000
- Name: Joint Photographic Expert Group	2000
- Developed in 2000 by the Joint Photographic Expert Group
- File extenstion: .jp2, .jpx
- Lossless and lossy compression
- Can handle transparency ($B=4$)
- Maximum size: $2^{32} \times 2^{32}$
- 38 bits/band
:::

:::{dropdown} PNG
- Name: Portable Network Graphics
- Developed in 1996 by the PNG Group
- File extenstion: .png
- Lossless compression
- Can handle transparency ($B=4$)
- Maximum size: $2^{31} \times 2^{31}$
- 16 bits/band
:::

:::{dropdown} TIFF
- Name: Tagged Image File Format
- Developed in 1986 by Aldus
- File extenstion: .tiff	
- Lossless or lossy compression
- Can handle transparency ($B=4$)
- Maximum size: $2^{32} \times 2^{32}$
- 16 bits/band
:::

The notions of lossless and lossy compressions are detailed in @P:compression:intro.

Although widely used, file formats such as SVG (Scalable Vector Graphics) and EPS (Encapsulated PostScript) are vector graphics and are not covered in this textbook.
The data is not stored by using an array as defined in @P:digital-images:definition:definition:
instead, these formats store data as mathematical instructions describing shapes.