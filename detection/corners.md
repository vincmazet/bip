# Corner detection

To detect the corners of objects in an image, one can start by detecting edges then determining where two edges meet.
There are however other methods, among which:
* the Moravec detector [[Moravec 1980](B:detection:Moravec1980)],
* the Harris detector [[Harris & Stephens 1988](B:detection:Harris1988)].

<!------------------------------------------------------------------------------------------------>

## Moravec detector

The principle of this detector is to observe if a sub-image, moved around one pixel in all directions, changes significantly.
If this is the case, then the considered pixel is a corner.

:::{figure} figs/corners-moravec.svg
:name: F:corners:moravec
Principle of Moravec detector.
From left to right :
on a flat area, small shifts in the sub-image (in red) do not cause any change;
on a contour, we observe changes in only one direction;
around a corner there are significant changes in all directions.
:::

Mathematically, the change is characterized in each pixel $(m,n)$ of the image by
$E_{m,n}(x,y)$ which represents the difference between the sub-images for a translation $(x,y)$:

$$
  \forall\ m,n,x,y \qquad E_{m,n}(y,x) = \sum_{u,v} w_{m,n}(u,v) \big[f(u+y,v+x)-f(u,v)\big]^2
$$

where:

* $x$ and $y$ represent the translations in the four directions:
  $$
  (x,y) \in \{(1,0),\,(1,1),\,(0,1),\,(-1,1)\}.
  $$
  In @F:corners:moravec, only the two translations $(1,0)$ and $(0,1)$ are shown for simplicity
  
* $w_{m,n}$ is a rectangular window around pixel $(m,n)$,

* $f(u+y,v+x)-f(u,v)$ is the difference between the sub-image $f(u,v)$
  and the translated sub-image $f(u+x,v+y)$,

In each pixel $(m,n)$, the minimum of $E_{m,n}(y,x)$ in the four directions is kept and denoted $F_{m,n}$.
Finally, the detected corners correspond to the local maxima of $F_{m,n}$,
that is, at pixels $(m,n)$ where the smallest value of $E_{m,n}(x,y)$ is large.

It turns out that Moravec detector has several limitations.
First, $w$ is a binary window and therefore the detector considers all pixels in the window with the same weight.
When the noise in the image is high, it can lead to false corner detections.
Second, only four directions are considered.
Third, the detector remains very sensitive to edges because only the minimum of $E$ is considered.
For these reasons, Harris has proposed a detector to overcome these limitations.

<!------------------------------------------------------------------------------------------------>

## Harris detector

To avoid a noisy response, the rectangular window $w$ of the Moravec detector is replaced by a Gaussian window $w$
in the expression of $E_{m,n}(x,y)$.

To extend the Moravec detector to all directions (not only the initial four directions),
a Taylor series expansion is performed on the shifted sub-image $f(u+y,v+x)$:

$$
  f(u+y,v+x) \approx f(u,v) + y \,\partial_y f(u,v) + x \,\partial_x f(u,v)
$$

so :

$$
E_{m,n}(y,x) \approx \sum_{u,v} w_{m,n}(u,v) \big[ y \,\partial_y f(u,v) + x \,\partial_x f(u,v) \big]^2
$$

This expression can be written in the following matrix form:

$$
E_{m,n}(y,x) \approx
\begin{pmatrix} y & x \end{pmatrix}
M
\begin{pmatrix} y \\ x \end{pmatrix}
$$

where

$$
M = 
\begin{pmatrix}
  \sum_{u,v} w_{m,n}(u,v)(\partial_y f)^2  &  \sum_{u,v} w_{m,n}(u,v)\partial_y f \,\partial_x f \\
  \sum_{u,v} w_{m,n}(u,v)\partial_y f \,\partial_x f  &  \sum_{u,v} w_{m,n}(u,v)(\partial_x f)^2 \\
\end{pmatrix}
$$

If a corner is present at pixel $(m,n)$,
then the derivatives of $f$ are very large,
so $M$ has large coefficients,
so the eigenvalues $\lambda_1$ and $\lambda_2$ of $M$ are also very large.
Because the calculation of the eigenvalues can be cumbersome,
it is attractive to use other quantities related to the eigenvalues.
Harris propose to use the trace $\mathrm{tr}(M)=\lambda_1 + \lambda_2$
and determinant $\mathrm{det}(M)=\lambda_1 \lambda_2$ of the matrix $M$.
These values can be calculated easily:

$$
\mathrm{tr}(M) = M_{1,1} + M_{2,2}
\quad\text{and}\quad
\mathrm{det}(M) = M_{1,1}M_{2,2} - M_{1,2}M_{2,1}.
$$

Finally, Harris propose to calculate

$$
R = \mathrm{det}(M) - k (\mathrm{tr}(M))^2
$$

with $0.04 < k < 0.06$.
The values of $R$ are low in a flat regions, negative on edges, and positive on corners.
An example is given @F:corners:harris.

:::{figure} figs/harris-detector.svg
:width: 100%
:name: F:corners:harris
Harris detector.
The binary images represent the negative (contours), weak (flat areas) and positive (corners) values of the coefficient $R$.
:::
