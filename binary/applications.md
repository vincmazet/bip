(P:binary:applications)=
# Applications

The four morphological tools seen in @P:binary:mm are the elementary operations for more complex processing.
In this section, we focus on some specific processings,
others are given by [[Bloch 2005, chapter 6](B:binary:Bloch2005)].

<!------------------------------------------------------------------------------------------------>

(P:binary:top-hat-transform)=
## Top-hat transform 

The top-hat transformation (French: *transformée du chapeau haut-de-forme*) keeps in the image only the objects that are narrower than the structuring element.
There are two dual top-hat transforms:
* The white top-hat transform is defined as the difference between the image $I$ and its opening by the structuring element $E$:

  $$
  T_w = I \setminus I \circ E.
  $$
  
* The black top-hat transform is defined as the difference between the closing by the structuring element $E$ and the image:
 
  $$
  T_b = I \bullet E \setminus I.
  $$

@F:binary:top-hat shows the effect 
of a white top-hat transform (only the white objects narrower than the structuring element are kept)
and a black top-hat transform (only the black objects narrower than the structuring element are kept).
Note that the structuring element, present in the original image, is not kept because it is not narrower than itself.
The results also show many of very small artifacts that can be easily removed by discarding the objects whose size is smaller than a predefined threshold.

:::{figure} figs/top-hat.svg
:width: 100%
:name: F:binary:top-hat
Example of a white and black top-hat transforms with a disk of radius 3 pixels as structuring element
(the latter is visible in the bottom-right corner of the original image).
:::

<!------------------------------------------------------------------------------------------------>

(P:binary:granulometry)=
## Granulometry

Granulometry (French: *granulométrie*) successively selects particles of increasing sizes in a binary image.
It consists of successive openings of an image $I$ by a sequence of structural elements $E_k$ of increasing size
(usually, $E_k = \underbrace{E\oplus \ldots \oplus E}_{k{\mbox{ times}}}$) where $E$ is a disk).

At each stage of opening, the finer details are successively eliminated, and the area of the image is reduced
(the area is the total number of pixels in the objects.).

@F:binary:granulometry-plot shows the granulometry function obtained on the binary image of @F:binary:granulometry-images by openings with a disk of different sizes.
When the size of the opening corresponds to the characteristic size of most objects, a jump appears in the curve.

:::{figure} figs/granulometry-images.svg
:width: 500px
:name: F:binary:granulometry-images
The original image and the corresponding openings by the successive structuring element (a disk).
:::

:::{figure} figs/granulometry-plot.svg
:width: 500px
:name: F:binary:granulometry-plot
The granulometry function.
:::

<!------------------------------------------------------------------------------------------------>

(P:binary:hit-or-miss-transform)=
## Hit-or-miss transform

The hit-or-miss transform (French: *transformée tout-ou-rien*) is used to detect objects of a particular shape.
Contrary to the transformations seen so far, the hit-or-miss transform examines configurations where certain pixels verify a relationship with the object
and others verify a relationship with the complement of the object.
Thus the structuring element $E$ of this transformation is composed of two elements $E_1$ and $E_2$ (disjoint but with the same origin).

The result of the hit-or-miss transform is the intersection of the two sets given by:
* the erosion of the image by $E_1$: $I \ominus E_1$,
* the erosion of the image background by $E_2$: $I^\mathrm{c} \ominus E_2$

The hit-or-miss transform by the two structuring elements $E_1$ and $E_2$ is noted $I \otimes (E_1, E_2)$:

$$
   I \otimes (E_1, E_2)
   &= (I \ominus E_1) \cap (I^\mathrm{c} \ominus E_2) \\
   &= (I \ominus E_1) \cap (I \oplus E_2)^\mathrm{c}
$$

:::{figure} figs/hit-or-miss-toy.svg
:name: F:binary:hit-or-miss
Example of a hit-or-miss transform applied on the image $I$ by the structuring elements $E_1$ and $E_2$.
The origin of the structuring elements are marked by the blue dot.
Because the background outside $I$ is considered black,
then the background outside $I^\mathrm{c}$ is considered white,
hence some white pixels in $I^\mathrm{c} \ominus E_2$.
:::

<!-- Sometimes, the two structuring elements are combined into a single structuring element whose pixels have the following values:
* $1$: pixels that belong to the object to detect,
* $-1$: pixels that do not belong to the object to detect (*i.e* pixels of the background),
* $0$: unused pixels (also called "don't care pixels").

With this notation, the structuring element of the hit-or-miss transform in @hit-or-miss` writes

$$
  (E_1, E_2) =
  \begin{pmatrix}
    -1 & -1 & -1 & -1 \\
    -1 &  1 &  1 & -1 \\
    -1 & -1 & -1 & -1
  \end{pmatrix}
$$ -->

<!------------------------------------------------------------------------------------------------>

(P:binary:skeleton)=
## Skeleton

The skeleton (French: *squelette*) is a useful notion in pattern recognition:
it is a "compact" form of the objects (thin lines centered within the objects),
with the same number of connected components and the same number of holes.

From a structuring element $E$, let us define $\forall k \in \mathbb{N}^*$:

$$
E_k = \underbrace{E\oplus \ldots \oplus E} _{k{\mbox{ times}}}
$$

<!-- Lantuéjoul's formula -->

The skeleton $S(I)$ of image $I$ is defined as:

$$
S(I) = \bigcup_{k \in \mathbb{N}^*}
(I \ominus E_k) \setminus (I \ominus E_k) \circ E.
$$


:::{figure} figs/skeleton.svg
:name: F:binary:skeleton
:width: 500px
Skeleton of the image $I$.
:::

<!-- ## Thinning (amincissement), thickening (épaississement) -- besoin pour squeletteTwo new transformations are deduced from the all-or-nothing transformation:

The thinning of $X$ by the structuring element $T=(T_1,T_2)$ is defined by:

$$
X \circ T = X \ X \otimes T
$$

and the thickening by:

$$
X \odot T = X \cup X \otimes T
$$

Thinning, an anti-extensive operation, therefore removes from $X$ points that are in a particular configuration, selected by the all-or-nothing transformation. The appropriate structuring elements are those for which the origin belongs to $T_1$. On the contrary, thickening adds to $X$ the points selected by the all-or-nothing transformation and is an extensive operation. The appropriate structuring elements are those for which the origin belongs to $T_2$. These two transformations are dual to each other in the following sense:

$$
X \ocirc T = (X^C \odot T')^C
$$

with $T' = (T_2,T_1)$ if $T = (T_1,T_2)$.

There is a whole "alphabet" of structuring elements, called the Golay alphabet in hexagonal grid, which allows a wide variety of operations to be performed [Serra, 1982a]. For example
:
- if $T_1$ is the elementary structuring element on the grid considered and $T_2$ is empty, the all-or-nothing transformation is an erosion and the corresponding thinning extracts the boundary of the objects;
- if the configurations sought by the all-or-nothing transformation correspond to a point of the complement surrounded by points of the object forming a locally non-convex configuration, the corresponding thickening (applied iteratively until convergence) makes it possible to calculate the smallest discrete convex containing the initial object;
- if $T_1$ is the central point of the elementary structuring element and contains the others, the all-or-nothing transformation selects the isolated points of the object;
– etc.

We will see later that particular configurations make it possible to extract the skeleton of an object by thinning. -->