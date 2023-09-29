(compression:lossless)=
# Lossless compression

Here are two examples of lossless image compression.

## Run-length encoding

RLE (run-length encoding) replaces a sequence of pixels of the same color with the number of pixels in that sequence.
Therefore, the image {numref}`F:compression:rle` needs 9 bytes to be stored without any compression.
By reading the image column after column, the bytes are:

$$
  \begin{pmatrix} 0 & 0 & 0 & 255 & 255 & 255 & 255 & 128 & 128 \end{pmatrix}.
$$


```{figure} rle.svg
---
name: F:compression:rle
---
A 3 × 3 image.
```

We see 3 pixels with intensity 0, 4 pixels with intensity 255, and 2 pixels with intensity 128.
Thus the image is encoded in RLE with only 6 bytes:

$$
  \begin{pmatrix} 3 & 0 & 4 & 255 & 2 & 128 \end{pmatrix}.
$$

In this example, the compression rate is 6/9 = 2/3.

In computers, the BMP format is based on RLE compression.

## Lempel-Ziv-Welch Algorithm

The LZW algorithm (Lempel-Ziv-Welch, 1984) is an improvement of the LZ78 algorithm (1978).
It is used in format like GIF or TIFF.
Briefly speaking, the principle is to build a dictionary where the "words" are groups of pixels and to assign a code to each group.
The dictionary is build during the compression stage and depends on the image.

<!--
 The algorithm is the following one:
 Initialize the dictionary with all the possible intensities
 For each pixel:
   Look to the longest sequence in the dictionary that starts at this pixel
   Replace this sequence with the corresponding code
   Add to the dictionary the sequence followed by the next pixel -->
