(P:binary:mm)=
# Mathematical morphology

Mathematical morphology gathers several techniques based on set theory, lattice theory, and topology.
It was initially dedicated to binary images but has now been extended to grayscale images.
In this course, we limit the presentation to binary images,
therefore we consider that the objects in the image define a set of pixels.

<!------------------------------------------------------------------------------------------------>

## Set operations

Consider the two following sets $A$ and $B$:

:::::{grid} 1 1 2 2

::::{grid-item} 
Set $A$:
:::{figure} figs/set-A.png
:height: 200px
:::
::::

::::{grid-item}
Set $B$:
:::{figure} figs/set-B.png
:height: 200px
:::
::::

:::::

Then we have the following operations.

:::::{tab-set}

::::{tab-item} Complement
The complement of $A$ is denoted $A^\mathrm{c}$ and is the set of pixels that are not in $A$:
$$A^\mathrm{c} = \{p \notin A \}$$
:::{figure} figs/set-complement.png
:height: 200px
:::
::::

::::{tab-item} Union
The union $A \cup B$ is the set of pixels present in $A$ or $B$ or both:
$$A \cup B = \{p \in A \, \mathrm{or} \, p \in B \}$$
:::{figure} figs/set-union.png
:height: 200px
:::
::::

::::{tab-item} Intersection
The intersection $A \cap B$ is the set of pixels present simultaneously in $A$ and $B$:
$$A \cap B = \{p \in A \, \mathrm{and} \, p \in B \}$$
:::{figure} figs/set-intersection.png
:height: 200px
:::
::::

::::{tab-item} Difference
The (set) difference $A \setminus B$ is the set of pixels present in $A$ but not in $B$:
$$A \setminus B = \{ x \in A \, \mathrm{and} \, x \notin B \}$$
:::{figure} figs/set-difference.png
:height: 200px
:::
::::

:::::

<!------------------------------------------------------------------------------------------------>

## Structuring element

In addition to this, the operators of mathematical morphology need a so-called structuring element (french: *élément structurant*).
A structuring element $E$ is a set of pixels (equivalent to a binary image) associated with an origin.
Generally, the origin is located at the centre of the structuring element;
but it may be elsewhere, even outside the pixels of the structuring element.
In the sequel, we denote by $E_c$ the structuring element centered on the pixel $c$.

## Basic operations

(P:binary:dilation)=
### Dilation

Having an image $I$ and a structuring element $E_c$, the dilation (french: *dilatation*)
of $I$ by $E_c$ is noted $I \oplus E_c$.
The result of the dilation is obtained by moving the origin of the structuring element onto the white pixels of the image
and keeping the set of pixels of each displaced structuring element.

Mathematically speaking:

$$
  I \oplus E_c = \{ E_c \mid c \in I \}
$$

:::{figure} figs/dilation-toy.svg
:name: mm:dilation-toy
Example of dilation on a small image $I$ by the structuring element $E_c$
(with the origin $c$ is at the centre and represented by the blue dot).
:::

The structuring element is often described with a matrix.
So, the structuring element in @mm:dilation-toy is written as:

$$
E =
\begin{pmatrix}
0 & 1 & 0 \\
1 & 1 & 1 \\
0 & 1 & 0 \\
\end{pmatrix}.
$$

Note that the matrix does not consider the zero pixels surrounding the main part of $E$.

Dilation has the following properties:

* Dilation is a binary operation and is not linear.
  Therefore, it cannot be expressed as convolution (which is a linear mathematical operator).

* Dilation is associative, *i.e.* the application of two consecutive dilations can be done in any order:

  $$
    (I \oplus  E_1 ) \oplus  E_2 = (I \oplus  E_2) \oplus  E_1 = I \oplus  (E_1 \oplus E_2)
  $$
  
  (here, the subscripts 1 and 2 mean two different structuring elements.)

* Dilation is a monotonous operation since the relations of inclusions are conserved:

  $$
    I_1 \subseteq I_2  \quad\Rightarrow\quad  I_1 \oplus E_c \subseteq I_2 \oplus E_c
  $$


(P:binary:erosion)=
### Erosion

The erosion (french: *érosion*) of $I$ by $E_c$ is noted $I \ominus E_c$.
The result of the erosion is obtained by moving the structuring element into the white pixels of the image
and keeping only the origin of each displaced structuring element.

$$
  I \ominus E_c = \{ c \mid E_c \subseteq I\}
$$

:::{figure} figs/erosion-toy.svg
:name: F:mm:erosion-toy
Example of erosion on a small image $I$ by the structuring element $E_c$
(with the origin $c$ is at the centre and represented by the blue dot).
:::

Erosion has similar properties as dilation:

* Erosion cannot be expressed as convolution.

* Erosion is associative:

  $$
    (I \ominus E_1 ) \ominus E_2 = (I \ominus E_2) \ominus E_1 = I \ominus (E_1 \oplus E_2)
  $$
  
  Note that the result of two successive erosions is equivalent to an erosion
  whose structuring element is the *dilation* of the two structuring elements.

* Erosion is a monotonous operation:

  $$
    I_1 \subseteq I_2  \quad\Rightarrow\quad  I_1 \ominus E \subseteq I_2 \ominus E
  $$


### Duality

Dilation and erosion are dual operators.
Considering the background as the object and the object as the background (*i.e.* by working with the complement of the image),
the dilation is converted to erosion and vice versa:

$$
  I^\mathrm{c} \ominus E = (I \oplus E)^\mathrm{c} \\
  I^\mathrm{c} \oplus E = (I \ominus E)^\mathrm{c}
$$

## Composition of basic operators


(P:binary:opening)=
### Opening

Opening (french: *ouverture*) consists of an erosion followed by a dilation.
The erosion removes small objects but also decreases the size of bigger objects.
To avoid this, the result is dilated with the same structuring element.

$$
  I \circ E = (I \ominus E_c) \oplus E_c
$$

:::{figure} figs/opening-toy.svg
:name: F:mm:opening-toy
Example of an opening on a small image $I$ by the structuring element $E_c$
(with the origin $c$ is at the centre and represented by the blue dot).
:::

Opening is an idempotent operation, that is to say, applying twice the same opening gives the same result as only one opening:
$$
(I \circ E) \circ E = I \circ E
$$

(P:binary:closing)=
### Closing

Contrary to opening, closing (french: *fermeture*) is firstly a dilation, then an erosion.
Indeed, dilation closes holes but enlarges objects.
To avoid the widening of the objects, an erosion can be applied with the same structuring element.

$$
  I \bullet E = (I \oplus E) \ominus E
$$

:::{figure} figs/closing-toy.svg
:name: F:mm:closing-toy
Example of closing on a small image $I$ by the structuring element $E_c$
(with the origin $c$ is at the centre and represented by the blue dot).
:::

Similarly to opening, closing is an idempotent operation:

$$
(I \bullet E) \bullet E = I \bullet E
$$