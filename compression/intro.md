(P:compression:intro)=
# Compression


How many bytes are needed to code one second of Full HD video?

:::{dropdown} Solution
A Full HD video is characterized by images of size 1920 × 1080, each of the three channels (RGB) is coded with 1 byte, and there are 50 frames per second.

One second contains 1920 × 1080 × 3 × 50 = 311 040 000 bytes, or around 311 Mb.
Thus, a DVD (4,7 Gb) can store only 15 seconds of a movie... 😲
You would need more than 600 DVDs to watch a movie...
:::

This example shows the need for image compression!
The purpose of image compression is to encode the *information* contained in the image with fewer bytes than the original image.

OK, but how to quantify information?
In 1948, [Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon) proposed that an image or a message is very informative if it is unlikely.
It is still the mathematical definition of information today.

We distinguish two kinds of compression:

* With @P:compression:lossless, no information is lost during compression,
  *i.e.* the original image and the compressed image are perfectly identical.
  It is possible to reach a compression ratio up to 1/10
  (the size in bytes of the compressed image is 1/10 of the original one).
  
* In @P:compression:lossy, we accept to lose information during compression
  (while ensuring that the original image remains close to the original one).
  The compression ratio can reach up to 1/100!