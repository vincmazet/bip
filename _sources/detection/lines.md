# Line detection


```{margin}
Pronounce Hough as "[huff](https://www.google.com/search?q=pronounce+hough+transform)"
(see [discussion](https://groups.google.com/g/sci.image.processing/c/yvgEDLPcQww?pli=1)).
```

Line detection consists of detecting alignments of points on an image of contours.
The usual method for line detection is the Hough transform [[Hough 1962](B:detection:Hough1962)].
Like the Fourier transform, it transposes the image from the spatial domain to another domain,
where the information of interest is represented differently.
In this case, the lines in the spatial domain are transformed into points in the Hough domain.

The Hough transform is not restricted to lines and can be used to detect any shape with a mathematical parameterization.
The working process remains the same as for line detection, so the sequel focuses on line detection only.


## First parameterization

In the spatial domain $(x,y)$, a line is parameterized by its coefficients $a$ and $b$:

$$
y = a x + b.
$$

Thus, any line can be represented by the pair $(a,b)$.
This is Hough's idea: each line of the image can be represented by a point in the Hough domain $(a,b)$.
The Hough domain is also called the parameter space.

```{figure} hough-1.png
---
width: 450px
name: F:lines:hough-1
---
The Hough transform transforms a line in the image into a point in the parameter space.
```

Conversely, a point in the image is represented by a line in the parameter space (which has the equation $b = \alpha a + \beta$).

```{figure} hough-2.png
---
width: 450px
name: F:lines:hough-2

```
In particular, a constant line $b=\beta$ in the parameter space corresponds to a point of abscissa $x=0$ in the image.

```{figure} hough-3.png
---
width: 450px
name: F:lines:hough-3
```

Finally, if several points in the image are aligned, their respective lines in the parameter space intersect at a single point,
which defines the equation of the line connecting them.

```{figure} hough-5.png
---
width: 450px
name: F:lines:hough-5
```

On a computer, the parameter space is finite and discretized (it is called an "accumulator").
Consequently, certain lines of the image cannot be represented there (_e.g._ a vertical line for which $a=\infty$).
In consequence, another parameterization of lines needs to be used in practice.


## New parameterization

To avoid the aforementioned problem of the parameterization space $(a,b)$, the lines are defined from two other parameters:
* the distance $d$ of the segment connecting the origin with the point closest to the line (this segment is perpendicular to the line),
* the angle $\theta$ that this segment makes with the x-axis.

Each line of the image is therefore parameterized by the pair $(\theta,d)$ which corresponds to a point in the parameter space $(\theta,d)$.

```{figure} hough-50.png
---
width: 450px
name: F:lines:houghnew
---
New parameterization of the Hough transform.
```

<!-- Equation de la droite paramétrée ainsi -->

We can show that for each point $(x_i,y_i)$ of the image, a sinusoid of equation $d = x_i \cos(\theta) + y_i \sin(\theta)$
is associated in the space $(\theta,d)$.
The sinusoids corresponding to the points of the same line intersect at the point $(\theta^*,d^*)$ parameterizing this line.

The Hough transform algorithm is as follows:

::::{grid} 1 1 1 1
:gutter: 3

:::{grid-item-card} Algorithm: Hough transform
1. Get the result of an edge detection
1. Initialize an accumulator (as the discrete space of the parameters)
1. For each pixel in the edges:
   1. Determine the sinusoid corresponding to the points
   1. Increment the accumulator along this sinusoid
1. Search for the maxima in the accumulator
1. Deduce the line parameters
:::

::::

{numref}`F:lines:example` gives an example of a Hough transform on an image representing a square.

```{figure} hough-example.svg
---
name: F:lines:example
---
Hough transform associated with the image on the left.
The sinusoids intersect at four (very bright) points, each one is associated with the line with the same letter.
```

<!-- Autre exemple : Léo Letouzey + Thomas Chabrier 2008 http://gepasud.upf.pf/images/documents/Letouzey/perso/hough.pdf -->

Besides, it appears that the Hough transform is robust to noise and to occultation (it can detect partially covered objects)

As said above, the Hough transform can be extended to any parameterized object (circles, ellipses, etc.).
For example, a circle is parameterized by three parameters (the center coordinates and the radius),
then the corresponding Hough space is three-dimensional.

Because, the dimension of the accumulator is equal to the number of parameters,
the main drawback of this method is that the computing time and the memory used quickly become significant.