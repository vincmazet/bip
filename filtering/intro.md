(P:filtering)=
# Transforms & Filtering

:::{aside}
Filtering in image processing is a very precise notion
that differs from the filters proposed by some apps or software
(a Snapchat filter is a non-linear transformation of an image and cannot be written
as a convolution product).
:::

Filtering an image consists of applying a filter,
which is a linear operator, to each pixel of an image to modify its intensity.
The new intensity of the pixel depends on the original intensity and the intensity of neighboring pixels.
Thus, the filter is expressed as a matrix or, similarly, as an image.
To study the concept of filtering,
it is essential to start by introducing two mathematical tools.

The first tool is @P:filtering:convolution,
which is the mathematical operation to calculate the effect of a filter on an image.
The second tool is the @P:filtering:fourier,
which introduce the notion of "frequency" in an image to represents the image in the frequency domain.
Then @P:filtering:filtering presents some filters, which only keep certain frequencies of the image,
such as the low-pass and high-pass filters.