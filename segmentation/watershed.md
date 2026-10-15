# Watershed

<!------------------------------------------------------------------------------------------------>

## Principle

The concept of watershed considers the image as a topographic map:
high intensities in the image are the mountains and low intensities are the valleys.
The principal objectives of the watershed segmentation method
is to find the crest lines of the topographic map,
where a drop of water placed on one of these crest lines
would be equally likely to fall on one side or the other of the line.

:::{figure} figs/watershed-concept.svg
:width: 600px
:name: F:segmentation:watershed-concept
A grayscale image (left) and its 3D representation as a topographic map (right).
The crest line is the top of the mountain in the shape of a "o".
:::

The basic idea of watershed segmentation is to flood the topographic map
and letting water rise through the valleys at a uniform rate.
When the rising water of two distinct valleys is about to merge,
a dam is built to prevent the merging.
When water covers the entire surface of the image,
the dams correspond to the segmentation boundaries.

:::{figure} figs/watershed-animation.svg
:width: 600px
:name: F:segmentation:watershed-animation
Illustration of water flooding on a cut at row 150 (see {numref}`F:segmentation:watershed-cut`).
The number corresponds to the water level,
the dams are shown in red.
:::

:::{figure} figs/watershed-cut.svg
:width: 250px
:name: F:segmentation:watershed-cut
The grayscale image with the watershed boundaries (dams) shown in red.
The profile considered in {numref}`F:segmentation:watershed-animation` is plotted in green.
:::

<!-- 
Le principe de la ligne de partage des eaux est donc :
1. de construire la carte d'élévation,
1. de remplir progressivement d'eau chaque bassin versant : l'eau apparaît tout en bas du relief,
1. de faire monter le niveau de l'eau,
1. lorsque deux bassins se rejoignent, la ligne de partage des eaux est marquée comme frontière.

Algorithm:
* Calculate the gradient (or Laplacian) of the image.
* The pixels with the lowest intensity form the initial watersheds.
* For each intensity level $i$ :
* For each group of pixels of intensity $i$ :
* If adjacent to exactly one existing region: add these pixels in this region.
* If adjacent to several regions simultaneously: mark as watershed.
* Otherwise, start a new region.

Note: several algorithms exist, which lead to slightly different results.
-->

<!------------------------------------------------------------------------------------------------>

## Application to an image

Generally, the contours of the objects do not correspond to the crest lines,
so the watershed has to be applied to the gradient of the image (see {numref}`F:segmentation:watershed-ok`).

:::{figure} figs/cells-watershed-ok.svg
:width: 700px
:name: F:segmentation:watershed-ok
An image (left), its gradient (center), and the result given by the watershed.
The contours are computed by using the [Sobel filter](C:detection:sobel).
:::

<!------------------------------------------------------------------------------------------------>

## Limitations

One of the limitations of the watershed method appears when there are many local minima in the image:
the watershed leads to over-segmentation because each local minimum will produce a segment.
This phenomenon is illustrated {numref}`F:segmentation:watershed-oversegmentation`
where the image is the same as in {numref}`F:segmentation:watershed-ok`
but degraded by additive noise and JPEG.
Therefore the image gradient now presents some small local minima.

:::{figure} figs/cells-watershed-oversegmentation.svg
:width: 700px
:name: F:segmentation:watershed-oversegmentation
Degraded version of {numref}`F:segmentation:watershed-ok` (left),
its gradient (center), and the result given by the watershed (right).
Clearly, the result is not satisfactory.
:::

To reduce the number of segments, one can:
* manually choose the watersheds of interest with markers ({numref}`F:segmentation:watershed-markers`),
* smooth (with a low-pass filter) the gradient before applying the algorithm ({numref}`F:segmentation:watershed-smooth`),
* merge the local minima.

:::{figure} figs/cells-watershed-markers.svg
:width: 700px
:name: F:segmentation:watershed-markers
Same image as in {numref}`F:segmentation:watershed-oversegmentation` (left),
its gradient and the chosen markers (center), and the result given by the watershed (right).
:::

:::{figure} figs/cells-watershed-smooth.svg
:width: 700px
:name: F:segmentation:watershed-smooth
Same image as in {numref}`F:segmentation:watershed-oversegmentation` (left),
the gradient of a smoothed version of the image (center), and the result given by the watershed (right).
:::