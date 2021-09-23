# Composition of basic operators


(mm:opening)=
## Opening

Opening (french: _ouverture_) consists of an erosion followed by a dilation.
The erosion removes small objects but also decreases the size of bigger objects.
To avoid this, the result is dilated with the same structuring element.

$$
  I \circ E = (I \ominus E_c) \oplus E_c
$$

```{figure} opening-toy.svg
---
name: F:mm:opening-toy
---
Example of an opening on a small image $I$ by the structuring element $E_c$
(with the origin $c$ is at the centre and represented by the blue dot).
```

### Property

* Opening is an idempotent operation, that is to say, applying twice the same opening gives the same result as only one opening:

  $$
  (I \circ E) \circ E = I \circ E
  $$


(mm:closing)=
## Closing

Contrary to opening, closing (french: _fermeture_) is firstly a dilation, then an erosion.
Indeed, expansion closes holes but enlarges objects.
To avoid the widening of the objects, an erosion can be applied with the same structuring element.

$$
  I \bullet E = (I \oplus E) \ominus E
$$

```{figure} closing-toy.svg
---
name: F:mm:closing-toy
---
Example of closing on a small image $I$ by the structuring element $E_c$
(with the origin $c$ is at the centre and represented by the blue dot).
```

### Properties

* Similarly to opening, closing is an idempotent operation:
  
  $$
    (I \bullet E) \bullet E = I \bullet E
  $$


(mm:hit-or-miss)=
## Hit-or-miss transform

The hit-or-miss transform (french: _transformée tout-ou-rien_) is used to detect objects of a particular shape.
It is the intersection of the two sets given by:
* the erosion by a first structuring element $E_1$: $I \ominus E_1$,
* and the erosion of the background by a second structuring element $E_2$: $I^\mathrm{c} \ominus E_2$

with $E_1 \cap E_2 = \varnothing$ (the structuring elements must be disjointed).

$$
   I \otimes (E_1, E_2)
   &= (I \ominus E_1) \cap (I^\mathrm{c} \ominus E_2) \\
   &= (I \ominus E_1) \cap (I \oplus E_2)^\mathrm{c}
$$

```{figure} hit-or-miss-toy.svg
---
name: hit-or-miss
---
Example of a hit-or-miss transform applied on image $I$ by the structuring elements $E_1$ and $E_2$.
The origins of the structuring elements are marked by a blue dot.
```

Sometimes, the two structuring elements are combined into a single structuring element whose pixels have the following values:
* $1$: pixels that belong to the object to detect,
* $-1$: pixels that do not belong to the object to detect (_i.e_ pixels of the background),
* $0$: unused pixels (also called "don't care pixels").

With this notation, the structuring element of the hit-or-miss transform in {numref}`hit-or-miss` writes

$$
  (E_1, E_2) =
  \begin{pmatrix}
    -1 & -1 & -1 & -1 \\
    -1 &  1 &  1 & -1 \\
    -1 & -1 & -1 & -1
  \end{pmatrix}
$$


<!-- Aller plus loin dans les notions vues, avec extension en niveau de gris (cf dans Jahne) ou présentation des fonctions supplémentaires disponibles dans scikit-image. Inclure par exemple : top-hat filter, transformée de distance (dans Jahne ?), épaissisement (thickening), amainsissement (thinning), squeletisation (skeletons), taillage (pruning), représentation de l'image sous forme d'un arbre... -->