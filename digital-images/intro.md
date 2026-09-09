(P:digital-images:intro)=
# Digital images

A digital image is a visual representation of a numerical array that measures a physical phenomenon.
This introductory chapter begins by describing the principles of digital image acquisition,
followed by a detailed definition of digital images,
and concludes with some essential visualization and analysis tools.

The human eye contains specific cells (cones) that are sensitive to color.
Traditional image acquisition devices mimic this process by using colored filters placed in front of photodiodes
which convert light intensity into electrical voltage.
This explains why screens — and by extension, most images — are encoded using three channels corresponding to red, green, and blue.

So, a digital image is a matrix of numbers with a graphical representation.
Each number in this matrix corresponds to the light intensity and color of a specific element in the image (the so-called pixel).
However, images are not limited to two dimensions and can also be multiband.

Image quality is influenced by factors such as sampling, quantization, and various distortions like noise or blur.
Because digital images are essentially numerical arrays, we can perform basic mathematical operations on them, such as addition, subtraction, and division.
Lastly, we will introduce the concept of the histogram, which represents the distribution of image intensities,
as well as some intensity transformations that can be applied.