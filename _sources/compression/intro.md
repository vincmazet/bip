# Introduction

<!-- Afficher en sur-impression les images des coefficients de la DCT sur la grille des coefficients. -->
<!-- Afficher l'image de différence en plus de l'originale et de la transformée. -->

How many bytes are needed to code one second of Full HD video?
A Full HD video is characterized by images of size 1920 × 1080, each of the three channels (RGB) is coded with 1 byte, and there are 50 frames per second.

```{dropdown} Solution
One second contains 1920 × 1080 × 3 × 50 = 311 040 000 bytes, or around 311 Mb.
Thus, a DVD (4,7 Gb) can store only 15 seconds of a movie... 😲
You would need more than 600 DVDs to watch _Harry Potter and the philosopher's stone_...
```

This example shows the need for image compression!
The purpose of image compression is to encode the _information_ contained in the image with fewer bytes than the original image.
OK, but how to quantify information?
In 1948, [Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon) proposed to consider that an image or a message is very informative if it is unlikely.
It is still the mathematical definition for information.

We distinguish two kinds of compression:

* With [](compression:lossless), no information is lost during compression,
  _i.e._ the original image and the compressed image are perfectly identical.
  It is possible to reach a compression ratio up to 1/10
  (the size in bytes of the compressed image is 1/10 times the original one).
  
* In [](compression:lossy), we accept to lose information during compression
  (while ensuring that the original image remains close to the original one).
  The compression ratio can reach 1/100!