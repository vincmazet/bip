(P:binary:measure)=
# Measure

It is possible to measure the geometric characteristics of the objects in a binary image,
such as the area or position.
In scikit-image, the most common properties are implemented in `skimage.measure`, especially in the function `regionprops`.
This section lists some of them, as an example of possibilities.

## Area

Area of an object is the number of pixels of this object.
The larger the object and the fewer holes it contains, the larger the area.

:::{figure} figs/prop-area.svg
:width: 500px
:align: center
:::

## Bounding box

The bounding box (french: *boîte englobante*) is the smallest rectangle that contains the object.

:::{figure} figs/prop-bbox.svg
:width: 500px
:align: center
:::

## Centroid

The centroid is the centre of gravity of the object.
It can be outside the object.

:::{figure} figs/prop-centroid.svg
:width: 500px
:align: center
:::

## Eccentricity

Eccentricity measures the elongation, or stretching, of the object, as it would be an ellipse.
It is a positive value, where 0 corresponds to a round object.

:::{figure} figs/prop-eccentricity.svg
:width: 500px
:align: center
:::

## Solidity

Solidity is the ratio of pixels in the objects to pixels of the [convex hull](https://en.wikipedia.org/wiki/Convex_hull) image.
It gives a measure of the compactness of the object.
In the image below, the convex hull is shown in green.

:::{figure} figs/prop-solidity.svg
:width: 500px
:align: center
:::

