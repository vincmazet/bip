# Histogram thresholding


## Binary thresholding

A very simple method of segmentation consists in associating with each pixel of the image $f$
a binary number which depends on the intensity of the pixels and on a threshold (french: _seuil_) $T$:

$$
  g(m,n) =
  \begin{cases}
    1 & \text{if}\, f(m,n)\geqslant T, \\
    0 & \text{if}\, f(m,n)<T
  \end{cases}
$$

This method is called "binarization" (french: _binarisation_).
It gives a segmentation into two classes, depending on the intensity of the pixels of a grayscale image
({numref}`F:segmentation:binarization`).


```{figure} binarization.svg
---
name: F:segmentation:binarization
height: 300px
---
Example of binarization for two thresholds.
```

As you can see, the segmentation depends on the value of $T$.
Therefore, the histogram is very useful to choose the threshold!
As an example, {numref}`F:segmentation:binarization-histogram` gives the histogram of the image, with the chosen thresholds.


```{figure} binarization-histogram.svg
---
name: F:segmentation:binarization-histogram
---
Histogram of {numref}`F:segmentation:binarization` with the two thresholds.
```

Now, it would be useful to have an automatic process to define the threshold, whatever the image to segment.
Otsu's method is the most famous automatic method for histogram thresholding.


(segmentation:otsu)=
## Otsu's method

Binarization divides the histogram of the images in two groups, namely class 0 and class 1, as illustrated {numref}`F:segmentation:otsu-histogram`.

```{figure} otsu-histogram.svg
---
name: F:segmentation:otsu-histogram
---
An histogram and a threshold $T$.
```

Each group has a number of pixel $w_i(T)$ with mean $\mu_i(T)$ and variance $\sigma_i^2(T)$.
Otsu's method (1979) computes the threshold $T$ which minimizes the intra-class variance $\sigma_w^2(T)$
(also known as the within-class variance),
defined as the weighted mean of the variances of each class:

$$
  \sigma_w^2(T) = w_0(T)\sigma_0^2(T) + w_1(T)\sigma_1^2(T).
$$

Considering the intensities to lie in $\{0,\dots,L-1\}$ and $h$ the histogram, the variables are defined as below.


````{panels}
:column: col-lg-6 col-md-6 col-sm-12 col-xs-12 p-2

Class 1
^^^
$\displaystyle w_0(T) = \sum_{i = 0}^{T} h(i)$

$\displaystyle \mu_0(T) = \frac{1}{w_0(T)} \sum_{i = 0}^{T} i h(i)$

$\displaystyle \sigma^2_0(T) = \frac{1}{w_0(T)} \sum_{i = 0}^{T}(i-\mu_0(T))^2 h(i)$

---

Class 2
^^^
$\displaystyle w_1(T) = \sum_{i = T+1}^{L-1} h(i)$

$\displaystyle \mu_1(T) = \frac{1}{w_1(T)} \sum_{i = T+1}^{L-1} i h(i)$

$\displaystyle \sigma^2_1(T) = \frac{1}{w_1(T)} \sum_{i = T+1}^{L-1}(i-\mu_1(T))^2 h(i)$

````

The algorithm to determine the value of $T$ that minimize $\sigma_w^2(T)$ is simple:
the intra-class variance $\sigma_w^2(T)$ is calculated for all the thresholds $T=\{0,\dots,L-1\}$,
and the one that gives the lowest value for $\sigma_w^2(T)$ is returned.

An example of Otsu's thresholding is given {numref}`F:segmentation:otsu`.

```{figure} otsu.svg
---
name: F:segmentation:otsu
height: 300px
---
Result of Otsu's segmentation.
```


## Multiple threshold

An image can be segmented in more than two classes by defining or computing several thresholds (see {numref}`F:segmentation:multiple-thresholds`).
In particular, Otsu's method can be extended to several thresholds,
but the computational complexity (hence the computation time) increases greatly with the number of classes!

```{figure} multiple-thresholds.svg
---
name: F:segmentation:multiple-thresholds
height: 300px
---
Several thresholds are applied to an image to get several classes (shown in colors).
```

<!-- 
En TP ?
La variation d'illumination ne permet pas de seuiller correctement l'image. Plusieurs solutions sont possibles.
TODO : afficher :
- image originale + son histogramme + son seuillage
- fond
- image sans fond + son histogramme + son seuillage
[image : seuillage_variation_illumination, \imgref{Gonzalez $\&$ Woods}

Éclairage $g$ connu : on utilise un modèle paramétrique pour le décrire et on corrige l'image avant le seuillage :
$$
\forall (m,n), \quad  h(m,n) = \frac{f(m,n)}{g(m,n)}
$$
* Éclairage $g$ inconnu : seuillage local par exemple
  \includegraphics[width=8.5cm]{seuillage_bloc}
  \imgref{Gonzalez $\&$ Woods}
\pnode(3.8,1.2){A}
\rput[lt](2,0.3){\rnode{B}Attention : zone à une seule classe ($\Rightarrow$ test de la variance)}
\ncline[linecolor=gray]{<-}{A}{B}

Influence du bruit
Ajout d'un bruit gaussien sur l'image $\Rightarrow$ convolution de l'histogramme de l'image par une gaussienne.
  \includegraphics[width=10cm]{seuillage_bruit}
  \imgref{Gonzalez $\&$ Woods}
Solutions possibles :
* Débruiter l'image initiale (filtre gaussien, filtre moyenneur, méthode de débruitage, ...)
* Filtrer l'image seuillée (opérateurs morphologiques, filtre médian, ...)
  \only<2>{\rput[c](.5\linewidth,-2){\includegraphics[width=8cm]{vincent72}}}
* Incorporer de l'information spatiale dans la méthode de segmentation.
  \includegraphics[width=10cm]{seuillage_filtre_median} -->