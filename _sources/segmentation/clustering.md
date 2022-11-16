# Clustering

Thresholding apply well on a grayscale image, for which it is easy to define a threshold from the modes of the histogram.
However, this approach cannot be applied on a color or multiband image because there is no histogram.
Each pixel in a $B$-band image can be represented by a point in a $B$-dimensional space.
By doing so, pixels with similar colors form groups in the space, as illustrated in {numref}`F:segmentation:clustering`.

```{figure} figs/3d-space.svg
---
name: F:segmentation:clustering
width: 100%
---
Showing the pixels of a color image in a $B$-dimensional space.
```

```{margin}
In French, these methods are called _méthodes de classification_, although it would be more precise to call them _méthode de coalescence_.
```

Clustering methods consists in defining groups of pixels.
Therefore, all the pixels in the same group define a class in the segmented image.

A classical clustering method for image segmentation is the k-means method (French: _k-moyennes_).

The k-means algorithm [[Steinhaus 1957](B:segmentation:Steinhaus1957), [MacQueen 1967](B:segmentation:MacQueen1967)]
is an iterative method that affects every point in the space $\mathbb{R}^B$ to a group (called cluster).
The number $K$ of groups is chosen by the user.
In the sequel, the centroid defines the center of a group.
Its coordinates are the mean of the coordinates of the points in the group.

The algorithm is given below.

::::{grid} 1 1 1 1
:gutter: 3

:::{grid-item-card} Algorithm: K-means
1. Initialize (randomly) the $K$ centroids
1. While the centroids vary:
   1. {bdg-info-line}`STEP A` For each point:
      1. Calculate the distances from the point to all centroids
      1. Assign the point to the nearest group
   1. {bdg-info-line}`STEP B` Calculate the centroid of each group
:::

::::

```{margin}
[A funny illustration of the K-means algorithm](https://allisonhorst.com/k-means-clustering).
```

{numref}`F:segmentation:kmeans-algo` illustrate this algorithm,
in the simple case of an image with two bands (hence the two-dimensional space)
segmented into $K=2$ classes.

```{figure} k-means-algorithm.svg
---
width: 100%
name: F:segmentation:kmeans-algo
---
Illustration of the k-means algorithm (click to enlarge).
```

{numref}`F:segmentation:kmeans-result` gives the result of the k-means algorithm on an image.

```{figure} segmentation-kmeans-result.png
---
height: 200px
name: F:segmentation:kmeans-result
---
Segmentation with the k-means algorithm on the left image (center: $K=2$ classes, right: $K=4$ classes).
```

The pros and cons of the k-means method for image segmentation are listed below.

::::{grid} 1 1 2 2
:gutter: 3

:::{grid-item-card} 😀 Advantages
* simplicity
* easy to implement
* generally fast
* works correctly when the clusters are spherical*
:::

:::{grid-item-card} ☹️ Disadvantages
* requires to know the number of classes
* sensitive to initialization
* can be slow in large dimensions
* fails for non-spherical structures*
* sensitive to outliers*
:::

::::

The characteristics above identified with * are now detailed.

Because the k-means algorithm performs the grouping with respect to the distance of the points to the centroids,
it assumes that the groups are sphericals.
Therefore, the algorithm works well for spherical clusters, but it fails if the clusters are not spherical,
as depicted in the images below.

```{figure} kmeans-ok.svg
---
height: 200px
name: F:segmentation:kmeans-ok
---
Spherical clusters: the k-means algorithm works well.
The points are depicted by $\bullet$ whose color correspond to the class,
and the centroids are depicted by a black $\times$.
```

```{figure} kmeans-croissants.svg
---
height: 200px
name: F:segmentation:kmeans-croissants
---
Non-spherical clusters: the k-means algorithm fails.
```

In addition to this, the centroids are calculated as the mean of the points in the cluster.
But the mean is not a robust estimation and is sensitive to points located far from the group.
Thus, the algorithm may fail in the presence of outliers (_valeurs aberrantes_).

```{figure} kmeans-outliers.svg
---
height: 200px
name: F:segmentation:kmeans-outliers
---
Presence of outliers: the k-means algorithm fails in this example.
```

Other clustering methods are available to avoid some of the aforementionned limits.
We can cite for example Gaussian mixture modeling or Mean-shift.
   

<!-- ### Modèles paramétriques


L'histogramme de l'image est modélisé par un mélange de lois \eng{mixture model} :
on dispose d'un modèle paramétrique représentatif des classes présentes dans l'image.

  \includegraphics[width=10cm]{vincent52}

* Lois : souvent gaussiennes \eng{GMM : Gaussian mixture model}.
* Extension possible à plusieurs dimensions

Deux étapes :
\begin{enumerate}
* Estimation des paramètres des lois
  {\color{gray}Poids $\Pi_k$, moyennes $\mu_k$, écart-types $\sigma_k$}
    \includegraphics[width=6cm]{vincent54}
* Classification
  {\color{gray}Associer à chaque intensité la classe la plus représentative}
\end{enumerate}

\paragraph{{\color{unistra}$\blacksquare$\hspace*{-.6em}\scriptsize\sf\raisebox{.5mm}{\color{white}1}}\; Estimation}

$$
  \forall i,\qquad
  p(h(i)|\theta) = \sum_{k=1}^K \frac{\Pi_k}{\sqrt{2\pi\sigma_k^2}} \exp\left(-\frac{(h(i)-\mu_k)^2}{2\sigma_k^2}\right)
$$

où $K$ est le nombre de classes
et $\theta$ regroupe les paramètres inconnus des lois :
$\theta=[\Pi_1,...,\Pi_K,\mu_1,...,\mu_K,\sigma_1,...,\sigma_K]$.

Estimation des paramètres au sens du maximum de vraisemblance :

$$
  \hat{\theta}^\text{MV} = \arg \max_{\theta} \prod_i p(h(i)|\theta)
$$

Méthode de résolution : algorithme EM, algorithmes MCMC, ...

\paragraph{{\color{unistra}$\blacksquare$\hspace*{-.6em}\scriptsize\sf\raisebox{.5mm}{\color{white}2}}\; Classification}

  \includegraphics[width=6cm]{vincent54}

Chaque pixel est affecté à la classe dont il maximise la loi :

$$
  f_\text{seg}(m,n) = \arg \max_{k\in\{1,...,K\}}
    \frac{\Pi_k}{\sqrt{2\pi\sigma_k^2}} \exp\left(-\frac{(f(m,n)-\mu_k)^2}{2\sigma_k^2}\right)
$$

\parbox{.45\textwidth}{\paragraph{k-moyennes}}
\parbox{.45\textwidth}{\paragraph{Mélange de gaussiennes}}

\parbox{.45\textwidth}{Estimation uniquement des $\mu_k$}
\parbox{.45\textwidth}{Estimation des $\mu_k$ et $\sigma_k$}

\parbox{.45\textwidth}{Sensible à l'initialisation}
\parbox{.45\textwidth}{Sensible à l'initialisation}

\parbox{.45\textwidth}{Sensible aux minima locaux}
\parbox{.45\textwidth}{Sensible aux minima locaux}

\parbox{.45\textwidth}{Nécessite de connaître le nombre de classes}
\parbox{.45\textwidth}{Nécessite de connaître le nombre de classes}

\parbox{.45\textwidth}{\centering\includegraphics[width=4cm]{vincent58-kmeans}}
\parbox{.45\textwidth}{\centering\includegraphics[width=4cm]{vincent58-gmm}} -->
