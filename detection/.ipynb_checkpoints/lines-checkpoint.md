# Line detection


```{margin}
Pronounce Hough as "[huff](https://www.google.com/search?q=pronounce+hough+transform)"
(see [discussion](https://groups.google.com/g/sci.image.processing/c/yvgEDLPcQww?pli=1)).
```

Line detection consists of detecting alignments of points in an image of contours.
The usual method for line detection is the Hough transform [[Hough 1962](B:detection:Hough1962)].
Like the Fourier transform, it transposes the image from the spatial space to another space,
where the information of interest is represented differently:
the lines in the spatial space are transformed into points in the Hough space.


## First parameterization

In the spatial space $(x,y)$, a line is parameterized by its coefficients $a$ and $b$,
giving the equation $y = a x + b$.
Thus, any line can be identified by the pair $(a,b)$.
This is Hough's idea: each line of the image can be represented by a point in the Hough space $(a,b)$.
The Hough space is then called the parameter space.


```{figure} hough-ab-0.svg
---
width: 500px
name: F:lines:hough-1
---
The Hough transform transforms a line in the image into a point in the parameter space.
```

Conversely, a point in the image is represented by a line in the parameter space.

```{figure} hough-ab-1.svg
---
width: 500px
name: F:lines:hough-2

```
In particular, a constant line $b=\beta$ in the parameter space corresponds to a point of abscissa $x=0$ in the image.

```{figure} hough-ab-2.svg
---
width: 500px
name: F:lines:hough-3
```

If several points in the image are aligned, their respective lines in the parameter space intersect at a single point,
which defines the equation of the line connecting them.

```{figure} hough-ab-3.svg
---
width: 500px
name: F:lines:hough-5
```

On a computer, the parameter space is finite and discretized (it is called an "accumulator").
Consequently, certain lines of the image cannot be represented,
such as a vertical line of slope $a=\infty$.
In consequence, another parameterization needs to be used in practice.


## New parameterization

To avoid the aforementioned problem of the parameterization space $(a,b)$, the lines are defined from two other parameters:
* the distance $d$ of the segment connecting the origin with the point closest to the line (this segment is perpendicular to the line),
* the angle $\theta$ of this segment with the x-axis.

Each line of the image is therefore parameterized by the pair $(\theta,d)$ which corresponds to a point in the parameter space $(\theta,d)$.

```{figure} hough-td-1.svg
---
width: 500px
name: F:lines:houghnew
---
New parameterization of the Hough transform.
```

<!-- Equation de la droite paramétrée ainsi -->

We can show that for each point $(x_i,y_i)$ of the image, a sinusoid of equation $d = x_i \cos(\theta) + y_i \sin(\theta)$
is associated in the space $(\theta,d)$.
The sinusoids corresponding to the points of the same line intersect at a unique point in the parameter space.

```{figure} hough-td-2.svg
---
width: 500px
name: F:lines:hough-td-2
```

The Hough transform algorithm is as follows:

::::{grid} 1 1 1 1
:gutter: 3

:::{grid-item-card} Algorithm: Hough transform
1. Compute an edge detection of the image
1. Initialize the accumulator (as the discrete space of the parameters)
1. For each pixel in the edges:
   1. Determine the sinusoid corresponding to the points
   1. Increment the accumulator along this sinusoid
1. Search for the maxima in the accumulator: they correspond to the parameters of the lines in the image
:::

::::

{numref}`F:lines:toy-example` gives an example of a Hough transform on an image representing a square.

```{figure} hough-toy-example.svg
---
name: F:lines:toy-example
---
Hough transform associated with the image on the left.
The sinusoids intersect at four (very bright) points, each one is associated with the line with the same letter.
```

{numref}`F:lines:example` gives an example of a Hough transform on an real photograph.

```{figure} hough-example.svg
---
name: F:lines:example
---
Hough transform associated with the image on the left.
```

<!-- Autre exemple : Léo Letouzey + Thomas Chabrier 2008 http://gepasud.upf.pf/images/documents/Letouzey/perso/hough.pdf -->

Besides, it appears that the Hough transform is robust to noise and to occultation (it can detect partially covered objects)

## Hough transform for other shapes

The Hough transform is not restricted to lines and can be used to detect any shape that has a mathematical parameterization: circles, ellipses, etc.

To detect other parametrized objectif with Hough transform,
the parameter space has to be adapted to the mathematical parameterization.
For example, a circle is parameterized by three parameters (the center coordinates and the radius),
then the corresponding Hough space is three-dimensional.

In consequence, as the dimension of the accumulator is equal to the number of parameters,
the main drawback of this method is that the computing time and the memory used quickly become significant for some shapes.