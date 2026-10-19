(P:binary:neighborhood)=
# Neighborhood and connectivity

In a usual image, a pixel at coordinates $(m,n)$ has four horizontal and vertical neighbors
whose coordinates are given by

$$
(m+1,n),\quad
(m-1,n),\quad
(m,n+1),\quad
(m,n-1).
$$

Considering these 4 neighbors, we speak of 4-connectivity (french: *4-connexité*).

Besides, there are also four diagonal pixels with coordinates

$$
(m+1,n+1),\quad
(m+1,n-1),\quad
(m-1,n+1),\quad
(m-1,n-1).
$$

These pixels, together with the 4-neighbors, are the 8 neighbors in 8-connectivity (french: *8-connexité*).

:::{figure} figs/neighborhood.svg
:height: 200px
:name: binary:neighborhood
The neighbors of the blue pixel are represented in green,
with 4-connectivity (left) and 8-connectivity (right).
:::

A path   between two pixels with coordinates $(m_1,n_1)$ and $(m_N,n_N)$ is a sequence of pixels
such that two consecutive pixels are neighbors in the considered connectivity.
Let $S$ represent a set of pixels in an image.
Two pixels are said to be connected if there exists a path between them consisting entirely of pixels in $S$.

The set of pixels that are connected is called a connected component (french: *composante connexe*).

:::{figure} figs/connectivity.svg
:height: 200px
:name: F:binary:connectivity
In this image, there are 2 connected components with 4-connectivity,
but only 1 connected component with 8-connectivity.
:::