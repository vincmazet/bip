(P:binary:intro)=
# Binary image processing

A binary image is an image whose pixels take only two values, typically 0 and 1
(but ​​it can be 0 or 255, False or True, black or white, etc.).
A binary image can result from a segmentation, and the techniques presented in this chapter can help to improve the result.

So, we consider that the images contain objects (represented by white pixels) on a background (black pixels),
as in @mm:mickey.

:::{figure} figs/set-union.png
:name: mm:mickey
Example of a binary image composed of an object (a famous mouse head) on a background.
:::

After a short section introducing the concepts of [neighborhood and connectivity](#P:binary:neighborhood),
the basic operators of mathematical morphology ([dilation](#P:binary:dilation) and [erosion](#P:binary:erosion),
and their combination [opening](#P:binary:opening) and [closing](#P:binary:closing)) are presented.
Multiple tools have been created from these operators, we focus on four of these tools:
[top-hat transform](#P:binary:top-hat-transform),
[granulometry](#P:binary:granulometry),
[hit-or-miss transform](#P:binary:hit-or-miss-transform),
and [skeleton](#P:binary:skeleton).
Finally, we deal with [measuring the geometric characteristics](#P:binary:measure) of binary objects.