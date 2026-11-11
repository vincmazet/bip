# Registration

:::{caution}

This chapter is currently being written and will be ready in a few days.

:::

<!--


 ## Introduction

Le recalage de deux images consiste à trouver la correspondance entre deux images représentant la même zone.
Les figures ci-dessous présentent quelques applications dans lesquelles le recalage est indispensable.

```{figure} vincent4.png
---
height: 250px
name: F:registration:remote-sensing
---
Recalage d'images de télédétection :
comment combiner ces deux acquisitions différentes de la même zone pour former une grande image ?
```

```{figure} vincent6.png
---
height: 250px
name: F:registration:medical
---
Recalage en imagerie médicale :
pour détecter des changements entre deux examens,
il faut que les images soient recalées (le patient n'est jamais exactement dans la même position).
```

```{figure} vincent13.png
---
height: 300px
name: F:registration:mosaicing
---
Mosaïque d'image (_image mosaicing_) :
combiner plusieurs images pour en faire une seule grande, en photographie.
```

La {numref}`F:registration:bigpicture` représente le schéma classique pour effectuer le recalage entre deux images.
Tout l'enjeu est d'estimer la transformation spatiale qui fait correspondre deux images.
Les différentes étapes représentées dans cette figure sont détaillées dans la suite de ce chapitre.

```{figure} bigpicture.png
---
height: 300px
name: F:registration:bigpicture
---
Schéma classique du recalage de deux images.
```

% Several scenarios
% •   Monomodal   vs  mul6modal   registra6on
% •   Registra6on of  2D/2D,  2D/3D,  3D/3D,  3D+t,   nD/nD   images
% •   Global  vs  local   /   rigid   vs  deformable  transforma6on


Nevertheless, the majority of the registration methods
consists of the following four steps (see Fig. 1):
† Feature detection. Salient and distinctive objects
(closed-boundary regions, edges, contours, line intersec-
tions, corners, etc.) are manually or, preferably, auto-
matically detected. For further processing, these features
can be represented by their point representatives (centers
of gravity, line endings, distinctive points), which are
called control points (CPs) in the literature.
† Feature matching. In this step, the correspondence
between the features detected in the sensed image and
those detected in the reference image is established.
Various feature descriptors and similarity measures
along with spatial relationships among the features are
used for that purpose.
† Transform model estimation. The type and parameters of
the so-called mapping functions, aligning the sensed
image with the reference image, are estimated. The
parameters of the mapping functions are computed by
means of the established feature correspondence.
† Image resampling and transformation. The sensed
image is transformed by means of the mapping
functions. Image values in non-integer coordinates
are computed by the appropriate interpolation
technique. 



 Geometric transformation ? rescale/resize, rotation, translation, stretch, shearing... (cf Jahne fig 10.16 p. 277 + fig 10.15 p. 276) 


-->