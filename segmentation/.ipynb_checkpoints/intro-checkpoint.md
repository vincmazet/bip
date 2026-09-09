(C:segmentation:intro)=
# Introduction

<!-- //// **AUTRE**
some basic relationship between pixels
- neigbors of a pixel
- adjancy, connectivity, regions and boundaries
- distance measure
//// -->

Image segmentation consists in partitioning an image $f$ according to a certain criterion.
This means that the image is divided into regions $R_i$
that are both mutually disjoint and collectively cover the entire image.
Two pixels in the same region satisfy the criterion, but two pixels in two adjacent regions do not.

The figures below show several examples of segmentation.

```{figure} example-cells.png
---
name: F:segmentation:example-cells
---
Example of segmentation on gray levels
(left: original image, right: segmentation given as regions).
```

```{figure} example-daisy.png
---
name: F:segmentation:example-daisy
---
Example of segmentation on color
(left: original image, right: segmentation given as regions,
the colors of regions is the mean color of the pixels in the original image).
```

```{figure} example-haiti.png
---
name: F:segmentation:example-haity
---
Example of segmentation on color with a constraint of the region size
(left: original image, right: segmentation given as borders).
```

```{figure} example-mammo.png
---
name: F:segmentation:example-mammo
---
Example of segmentation on color
(left: original image, right: segmentation given as regions).
```

<!-- Ajouter un exemple avec comme critère la texture. Cf par ex https://scikit-image.org/docs/dev/auto_examples/features_detection/plot_glcm.html -->

The result of segmentation is not unique:
it depends on the criterion, the segmentation method, the initialization of the method, etc.
There are a lot of diverse segmentation methods and this chapter focuses on the more usual ones.
Finally, we talk about how to measure the quality of segmentation.

<!--
  Dire qu'il y a plein de manière de catégoriser les méthodes.
  Pour ma part, j propose une classification qui m'arrange.
  Présenter les liens avec une carte mentale ?
  Renseignements :
    - https://pequan.lip6.fr/~bereziat/pima/2012/seuillage/sezgin04.pdf
    - Wikipedia 
    - webdocs.cs.ualberta.ca/ nray1/CMPUT605/track3_papers/Threshold_survey.pdf
      "We categorize the thresholding methods in six groups according to the information they are exploiting:
      1. histogram shape-based methods (eg the peaks, valleys and curvatures of the smoothed histogram are analyzed)
      2. clustering-based methods (the gray-level samples are clustered in two parts or alternately are modeled as a mixture of two Gaussians)
      3. entropy-based methods (entropy of the foreground and background regions, cross-entropy between original and binarized image, etc.)
      4. object attribute-based methods (search a measure of similarity between the gray-level and the binarized images)
      5. the spatial methods (higher-order probability distribution and/or correlation between pixels)
      6. local methods (adapt the threshold value on each pixel to the local image characteristics)"
-->

<!--
  Autres méthodes de que je pourrais présenter :
    - par texture
    - Mean-shift {Fukunaga75}
    - SLIC {Achanta12}
    - Split/merge
    - Snakes
-->



<!-- <hr>

```{note}

La connexité est la façon dont sont définis les voisins d'un pixel.
En général, on n'utilise que l'une des deux connexités suivantes :
* la 4-connexité : un pixel possède quatre voisins (en haut, en bas, à gauche, à droite),
* la 8-connexité : un pixel possède huit voisins (les quatre précédents et ceux sur les diagonales).

figure figs/connexity.png
name: F:segmentation:connexity
4-connexité (à gauche) et 8-connexité (à droite). Les pixels en gris sont les voisins du pixel $(m,n)$.

Chaque région $R_i$ de la segmentation est une composante connexe.

Une composante connexe (_connected component_) est un groupe de pixels
tel qu'on puisse aller d'un pixel de ce groupe à un autre pixel de ce groupe
en passant par des pixels du même groupe voisins entre eux.

Ainsi, dans la {numref}`F:segmentation:connected-component`,
le nombre de composantes connexes est égal à 5 si on considère un voisinage en 4-connexité,
ou à 4 si on considère un voisinage en 8-connexité.

figure figs/connected-component.png
name: F:segmentation:connected-component
Le nombre de composantes connexes (entourées d'un trait de couleur) dépend de la connexité considérée.

``` -->