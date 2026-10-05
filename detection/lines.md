# Line detection


:::{margin}
Pronounce Hough as "[huff](https://www.google.com/search?q=pronounce+hough+transform)"
(see [discussion](https://groups.google.com/g/sci.image.processing/c/yvgEDLPcQww?pli=1)).
:::

Line detection consists of detecting alignments of points in an image of contours.
The usual method for line detection is the Hough transform [[Hough 1962](B:detection:Hough1962)].
Like the Fourier transform, it transposes the image from the spatial space to another space,
where the information of interest is represented differently:
the lines in the spatial space are transformed into points in the Hough space.

<!------------------------------------------------------------------------------------------------>

## First parameterization

In the spatial space $(x,y)$, a line is parameterized by its coefficients $a$ and $b$,
giving the equation $y = a x + b$.
Thus, any line can be identified by the pair $(a,b)$.
This is Hough's idea: each line of the image can be represented by a point in the Hough space $(a,b)$.

:::{figure} figs/hough-ab-0.svg
:width: 500px
:name: F:lines:hough-1
The Hough transform transforms a line in the image into a point in the parameter space.
:::

The Hough space is called the "parameter space".
On a computer, the parameter space is finite and discretized and is called the "accumulator".

In the same way, a point in the image is represented by a line in the parameter space.
<!-- expliquer pourquoi un point dans l'image devient une droite dans le domaine de Hough -->

:::{figure} figs/hough-ab-1.svg
:width: 500px
:name: F:lines:hough-2
:::
In particular, a constant line $b=\beta$ in the parameter space corresponds to a point of abscissa $x=0$ in the image.

:::{figure} figs/hough-ab-2.svg
:width: 500px
:name: F:lines:hough-3
:::

If several points in the image are aligned, their respective lines in the parameter space intersect at a single point,
which defines the equation of the line connecting them.

:::{figure} figs/hough-ab-3.svg
:width: 500px
:name: F:lines:hough-5
:::

But the parameterization has a major drawback:
a vertical line of slope $a=\infty$ cannot be represented.
So another parameterization needs to be used in practice.

<!------------------------------------------------------------------------------------------------>

## New parameterization

To avoid the aforementioned problem of the parameterization space $(a,b)$, the lines are defined from two other parameters:
* the distance $d$ of the segment connecting the origin with the point closest to the line (this segment is perpendicular to the line),
* the angle $\theta$ of this segment with the x-axis.

Each line of the image is therefore parameterized by the pair $(\theta,d)$ which corresponds to a point in the parameter space $(\theta,d)$.

:::{figure} figs/hough-td-1.svg
:width: 500px
:name: F:lines:houghnew
New parameterization of the Hough transform.
:::

We can show that for each point $(x_i,y_i)$ of the image, a sinusoid of equation $d = x_i \cos(\theta) + y_i \sin(\theta)$
is associated in the space $(\theta,d)$.
The sinusoids corresponding to the points of the same line intersect at a unique point in the parameter space.
This parameterization allows to model any type of traight line.

:::{figure} figs/hough-td-2.svg
:width: 500px
:name: F:lines:hough-td-2
:::

<!------------------------------------------------------------------------------------------------>

## Hough transform for line detection

The Hough transform algorithm is as follows:

:::{note} Hough transform
:icon: false
1. Initialize the accumulator (the discrete Hough space) with zeros.
1. For each pixel in the image:
   1. Determine the sinusoid corresponding to the points,
   1. Increment the accumulator along this sinusoid.
1. Search for the maxima in the accumulator: they correspond to the parameters of the lines in the image.
:::

The Hough transform applies on a binary (black and white) image with lines on a background.
Alternatively, if you search for straight borders in the image, you must first compute an @P:detection:edge of the image.

For example, consider the problem of searching for the borders on the diamond in @F:lines:toy-example:
an edge detection is first applied on the image, then the accumulator of the Hough transform shows four bright spots,
corresponding to the four edges of the shape.

:::{figure} figs/hough-toy-example.svg
:name: F:lines:toy-example
Hough transform associated with the image on the left.
The sinusoids intersect at four (very bright) points, each one is associated with the line with the same letter.
In particular, A is a line at distance 50 from the origin $(0,0)$ and its normal make a angle of 45°.
:::

@F:lines:example gives an example of a Hough transform on a real photograph.

:::{figure} figs/hough-example.svg
:name: F:lines:example
Hough transform applied on a real image.
The green circles identify the three brighter points in the accumulator.
:::

Besides, it appears that the Hough transform is robust to noise and to occultation (it can detect partially covered objects)

<!------------------------------------------------------------------------------------------------>

## Hough transform for other shapes

The Hough transform is not restricted to lines and can be used to detect any shape that has a mathematical parameterization: circles, ellipses, etc.

To detect other parametrized objectif with Hough transform,
the parameter space has to be adapted to the mathematical parameterization.
For example, a circle is parameterized by three parameters (the center coordinates and the radius),
then the corresponding Hough space is three-dimensional.

In consequence, as the dimension of the accumulator is equal to the number of parameters,
the main drawback of this method is that the computing time and the memory used quickly become significant for some shapes.