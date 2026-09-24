# Conclusion

Before introducing the concept of filtering, two mathematical tools are introduced in this chapter.

The first tool is the convolution product, denoted $*$,
which calculates the transformation $f = g*h$ of an image $g$ by a filter $h$.
The images $f$, $g$ and $h$ are expressed as matrices, not necessarily of the same size.

The second tool is the Fourier transform.
It is a linear operator that returns an image of the same size as the original image
and with the same information as the original image,
although the information is represented in frequency space rather than the spatial space.
In general, the output of the Fourier transform is an image with complex values ​
where the low frequencies are in the center and the high frequencies are on the periphery.
The Fourier transform could be used to analyze the frequency content of an image,
as we will see in @P:denoising and @P:deconvolution.

Filtering an image consists of applying a filter (also called PSF for point spread function) to an image.
In practice, filtering is the result of a convolution (in the spatial domain)
or a multiplication (in the frequency domain, via the Fourier transform).
Filtering could be applied to blur an image (low-pass filter)
or highlight the contours (high-pass filter).
Other filters are also possible.

A question remains:
is there an inverse convolution operator, like division is the inverse of multiplication?
The answer is generally no.
Practically, the quantification in the image, the presence of noise and the lack of knowledge of the PSF make the problem hard,
justifying the specific processing of @P:deconvolution to deal with.


:::{seealso} References

* (B:filtering:Jahne2005)=
  B. Jähne,
  *Digital Image Processing*,
  Springer, 2005.

* (B:filtering:Shannon1948)=
  C.E. Shannon,
  "A Mathematical Theory of Communication",
  *Bell System Technical Journal*,
  vol. 27, pp. 379-423, 1948.
:::