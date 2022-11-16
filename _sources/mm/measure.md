(mm:measure)=
# Measure

It is possible to measure the geometric characteristics of the objects in a binary image,
such as the area or position.
In scikit-image, the most common properties are implemented in `skimage.measure`, especially in the function `regionprops`.
This section list some of them, as an example of possibilities.

## Area

```{image} prop-area.svg
:width: 500px
:align: center
```
<br />

Area of an object is the number of pixels of this object.
The larger the object and the fewer holes it contains, the larger the area.

## Bounding box

```{image} prop-bbox.svg
:width: 500px
:align: center
```
<br />

The bounding box (french: _boîte englobante_) is the smallest rectangle that contains the object.

## Centroid

```{image} prop-centroid.svg
:width: 500px
:align: center
```
<br />

The centroid is the centre of gravity of the object.
It can be outside the object.

## Eccentricity

```{image} prop-eccentricity.svg
:width: 500px
:align: center
```
<br />

Eccentricity measures the elongation, or stretching, of the object, as it would be an ellipse.
It is a positive value, where 0 corresponds ot a round object.

## Solidity

```{image} prop-solidity.svg
:width: 500px
:align: center
```
<br />

Solidity is the ratio of pixels in the objects to pixels of the [convex hull](https://en.wikipedia.org/wiki/Convex_hull) image.
It gives a measure of the compactness of the object.

