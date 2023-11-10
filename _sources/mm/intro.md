(mm:intro)=
# Introduction

<!-- Dans le Jahne : quelques exos et interactivités -->

Mathematical morphology gathers several techniques that apply to binary images,
the latter result for example from thresholding.
The pixels in binary images take only two values: 0 or 1, true or false, white or black, etc.
In this chapter, we consider that the images contain objects (represented by white pixels) on a background (black pixels),
as in {numref}`mm:mickey`.

```{figure} set-union.png
---
name: mm:mickey
---
Example of a binary image composed of an object (a famous mouse head) on a background.
```

The basic operators of mathematical morphology, namely [dilation](mm:dilation) and [erosion](mm:erosion) are first presented.
The combination of these two operators allows the definition of new operators, namely [opening](mm:opening), [closing](mm:closing)
and the [hit-or-miss transform](mm:hit-or-miss).
A comparison of the operators is then presented.
At last, we deal with [measuring the geometric characteristics](mm:measure) of binary objects.

Before beginning, we need to introduce some basic notions.


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


## Neighborhood and connectivity

In a usual image, a pixel at coordinates $(m,n)$ has four horizontal and vertical neighbors
whose coordinates are given by

$$
(m+1,n),\quad
(m-1,n),\quad
(m,n+1),\quad
(m,n-1).
$$

Considering these 4 neighbors, we speak of 4-connectivity (french: _4-connexité_).

Besides, there exists also four diagonal pixels with coordinates

$$
(m+1,n+1),\quad
(m+1,n-1),\quad
(m-1,n+1),\quad
(m-1,n-1).
$$

These pixels, together with the 4-neighbors, are the 8 neighbors in 8-connectivity (french: _8-connexité_).

```{figure} neighborhood.svg
---
width: 400px
---
The neighbors of the green pixel are represented in red,
with 4-connectivity (left) and 8-connectivity (right).
```

A path between two pixels with coordinates $(m_1,n_1)$ and $(m_N,n_N)$ is a sequence of pixels
such that two consecutive pixels are neighbors in the considered connectivity.

Let $S$ represent a set of pixels in an image.
Two pixels are said to be connected if there exists a path between them consisting entirely of pixels in $S$.

The set of pixels that are connected is called a connected component (french: _composante connexe_).

```{figure} connectivity.svg
---
width: 200px
---
In this image, there are 2 connected components with 4-connectivity,
but only 1 connected component with 8-connectivity.
```


## Structuring element

In addition to this, the operators of mathematical morphology need a so-called structuring element (french: _élément structurant_).
A structuring element $E$ is a set of pixels (equivalent to a binary image) associated with an origin.
Generally, the origin is located at the centre of the structuring element;
but it may be elsewhere, even outside the pixels of the structuring element.
In the sequel, we denote by $E_c$ the structuring element centred on the pixel $c$.