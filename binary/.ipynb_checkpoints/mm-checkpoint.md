# Mathematical morphology


## Set operations

We also consider that the objects in the image define a set of pixels,
so mathematical morphology can use the usual operations on sets, listed below.
Consider $A$ and $B$ as two sets.

::::{grid} 1 1 2 3
:gutter: 3

:::{grid-item}
Set $A$:
```{figure} set-A.png
```
:::

:::{grid-item}
Set $B$:
```{figure} set-B.png
```
:::

::::

The **complement** of $A$ is denoted $A^\mathrm{c}$ and is the set of pixels that are not in $A$:

$$A^\mathrm{c} = \{p \notin A \}$$

```{figure} set-complement.png
```

The **union** $A \cup B$ is the set of pixels present in $A$ or $B$ or both:

$$A \cup B = \{p \in A \, \mathrm{or} \, p \in B \}$$

```{figure} set-union.png
```

The **intersection** $A \cap B$ is the set of pixels present simultaneously in $A$ and $B$:

$$A \cap B = \{p \in A \, \mathrm{and} \, p \in B \}$$

```{figure} set-intersection.png
```







## Structuring element

In addition to this, the operators of mathematical morphology need a so-called structuring element (french: _élément structurant_).
A structuring element $E$ is a set of pixels (equivalent to a binary image) associated with an origin.
Generally, the origin is located at the centre of the structuring element;
but it may be elsewhere, even outside the pixels of the structuring element.
In the sequel, we denote by $E_c$ the structuring element centred on the pixel $c$.








(mm:dilation)=
## Dilation

Having an image $I$ and a structuring element $E_c$, the dilation (french: _dilatation_)
of $I$ by $E_c$ is noted $I \oplus E_c$.
The result of the dilation is obtained by moving the origin of the structuring element onto the white pixels of the image
and keeping the set of pixels of each displaced structuring element.

Mathematically speaking:

$$
  I \oplus E_c = \{ E_c \mid c \in I \}
$$

```{figure} dilation-toy.svg
---
name: mm:dilation-toy
---
Example of dilation on a small image $I$ by the structuring element $E_c$
(with the origin $c$ is at the centre and represented by the blue dot).
```

The structuring element is often described with a matrix.
So, the structuring element in {numref}`mm:dilation-toy` is written as:

$$
E =
\begin{pmatrix}
0 & 1 & 0 \\
1 & 1 & 1 \\
0 & 1 & 0 \\
\end{pmatrix}.
$$

Note that the matrix does not consider the zero pixels surrounding the main part of $E$.


### Properties

* Dilation is a binary operation and is not linear.
  Therefore, it cannot be expressed as convolution which is a linear mathematical operator.

* Dilation is associative, _i.e._ the application of two consecutive dilations can be done in any order:

  $$
    (I \oplus  E_1 ) \oplus  E_2 = (I \oplus  E_2) \oplus  E_1 = I \oplus  (E_1 \oplus E_2)
  $$
  
  (here, the subscripts 1 and 2 mean two different structuring elements.)

* Dilation is a monotonous operation since the relations of inclusions are conserved:

  $$
    I_1 \subseteq I_2  \quad\Rightarrow\quad  I_1 \oplus E_c \subseteq I_2 \oplus E_c
  $$


(mm:erosion)=
## Erosion

The erosion (french: _érosion_) of $I$ by $E_c$ is noted $I \ominus E_c$.
The result of the erosion is obtained by moving the structuring element into the white pixels of the image
and keeping only the origin of each displaced structuring element.

$$
  I \ominus E_c = \{ c \mid E_c \subseteq I\}
$$

```{figure} erosion-toy.svg
---
name: F:mm:erosion-toy
----
Example of erosion on a small image $I$ by the structuring element $E_c$
(with the origin $c$ is at the centre and represented by the blue dot).
```

### Properties

Erosion has similar properties as dilation.

* Erosion cannot be expressed as convolution.

* Erosion is associative:

  $$
    (I \ominus E_1 ) \ominus E_2 = (I \ominus E_2) \ominus E_1 = I \ominus (E_1 \oplus E_2)
  $$
  
  Note that the result of two successive erosions is equivalent to an erosion
  whose structuring element is the _dilation_ of the two first structuring elements.

* Erosion is a monotonous operation:

  $$
    I_1 \subseteq I_2  \quad\Rightarrow\quad  I_1 \ominus E \subseteq I_2 \ominus E
  $$


## Duality

Dilation and erosion are dual operators.
Considering the background as the object and the object as background (_i.e._ by working with the complement of the image),
the dilation is converted to erosion and vice versa:

$$
  I^\mathrm{c} \ominus E = (I \oplus E)^\mathrm{c} \\
  I^\mathrm{c} \oplus E = (I \ominus E)^\mathrm{c}
$$










## Composition of basic operators


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

The hit-or-miss transform by the two structuring elements $E_1$ and $E_2$ is noted $I \otimes (E_1, E_2)$:

$$
   I \otimes (E_1, E_2)
   &= (I \ominus E_1) \cap (I^\mathrm{c} \ominus E_2) \\
   &= (I \ominus E_1) \cap (I \oplus E_2)^\mathrm{c}
$$

```{figure} hit-or-miss-toy.svg
---
name: hit-or-miss
---
Example of a hit-or-miss transform applied on the image $I$ by the structuring elements $E_1$ and $E_2$.
The origins of the structuring elements are marked by the blue and green dots.
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