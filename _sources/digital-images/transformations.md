(C:histogram-transformations)=
# Histogram transformations


An histogram transformation consists in applying a mathematical function to the intensity distribution.
Generally, the transformations are useful to improve the visual quality of an image,
but are rarely needed inside an automatic processing.

The transform, denoted $T$, is applied on the pixel intensities to change their values:

$$j = T(i)$$

where $j$ and $i$ are respectively the intensities of the new and the original image.
As a consequence, the histogram of the new image differs from the histogram of the original image.

Below are some common transformations (we suppose the pixel intensities to lie in $[0,1]$).


## Negative image

$$T(i) = 1-i$$

```{figure} negative.svg
---
name: F:histogram:negative
width: 80%
---
Negative image: the gray levels are reversed.
```

## Gamma correction

$$T(i) = i^\gamma$$

```{figure} gamma.svg
---
name: F:histogram:gamma
width: 80%
---

Gamma correction modify the coulours of an image acquired by an electronic system,
it is used to take into account the non-linear sensibility of human eyes to the light.
Here, $\gamma=0.4$
```


## Histogram spreading

(french: _étalement d'histogramme_)

$$T(i) = \frac{i-i_\text{min}}{i_\text{max}-i_\text{min}}$$

where $i_\text{min}$ and $i_\text{max}$ are respectively the minimum and maximum intensities in the image.

```{figure} spreading.svg
---
name: F:histogram:spread
width: 80%
---
Histogram spreading enhances the contrast by "dilating" the histogram to the whole intensity interval.
```


## Histogram equalization

(french: _égalisation d'histogramme_)

$$T(i) = \frac{1}{MN} \sum_{k=0}^i n_k$$

where $M$ and $N$ are the image size and $n_k$ is the number of pixels with intensity $k$.
This transformation aims to spread the histogram over the entire intensity range, and to make the histogram as flat as possible.
A consequence is an increasing of the image contrast.
It is a fully automatic method that does not require any parameters to be set.
The demonstration of this equation is available in {ref}`[Gonzalez 2010, section 3.3.1] <C:refs>`.

```{figure} equalization.svg
---
name: F:histogram:equalization
width: 80%
---
Histogram equalization is another contrast enhancing and tend to make the details more visible.
```

## Thresholding

The histogram is sometimes very useful to segment the image in two classes,
that is to distinguish the objects in the image with respect to their gray level.
Indeed, if the histogram shows clearly two modes (_i.e._ two "bumps"),
on can define a threshold $T$ between these two modes, then apply a thresholding on the pixels, such that:
* if the pixel level is lower that $T$, then the pixel is in class 0 (displayed in black in {numref}`F:histogram:threshold`),
* otherwise the pixel is in class 1 (displayed in white in {numref}`F:histogram:threshold`).

```{figure} thresholding.svg
---
name: F:histogram:threshold
width: 80%
---
Threshold with a threshold set to 0.45.
```

Such a thresholding yields a binary image whose pixels have only two values.
Several methods exist that compute automatically the threshold, such that {ref}`Otsu's method <C:segmentation>`.