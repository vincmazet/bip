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
The combination of these two operators allows defining [opening](mm:opening), [closing](mm:closing)
and the [hit-or-miss transform](mm:hit-or-miss).
A comparison of the operators is then presented.
At last, we deal with [measuring the geometric characteristics](mm:measure) of binary objects.

Before beginning, we need to introduce two notions.


## Set operations

We also consider that the objects in the image define a set of pixels,
so mathematical morphology can use the usual operations on sets, listed below.
Consider $A$ and $B$ as two sets.

````{panels}
:column: col-lg-4 col-md-6 col-sm-12 col-xs-12 p-2


Set $A$:

```{figure} set-A.png
```

---

Set $B$:

```{figure} set-B.png
```

````



````{panels}
:column: col-lg-4 col-md-6 col-sm-12 col-xs-12 p-2


The **complement** of $A$ is denoted $A^\mathrm{c}$ and is the set of pixels that are not in $A$:

```{figure} set-complement.png
```

$$
A^\mathrm{c} = \{p \notin A \}
$$

---

The **union** $A \cup B $ is the set of pixels present in $A$ or $B$ or both:

```{figure} set-union.png
```

$$
A \cup B = \{p \in A \, \mathrm{or} \, p \in B \}
$$

---

The **intersection** $A \cap B $ is the set of pixels present simultaneously in $A$ and $B$.:

```{figure} set-intersection.png
```

$$
A \cap B = \{p \in A \, \mathrm{and} \, p \in B \}
$$

````


## Structuring element

In addition to this, the operators of mathematical morphology need a so-called structuring element (french: _élément structurant_).
A structuring element $E$ is a set of pixels (equivalent to a binary image) associated with an origin.
Generally, the origin is located at the centre of the structuring element;
but it may be elsewhere, even outside the pixels of the structuring element.
In the sequel, we denote by $E_c$ the structuring element centred on the pixel $c$.