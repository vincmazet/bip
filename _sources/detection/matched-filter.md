# Matched filter

When a pattern (French: _motif_), perfectly known as a sub-image $g$, is searched for in an image $f$,
then the cross-correlation (French: _corrélation croisée_) between $f$ and $g$ is a very efficient technique.
This technique is often known as matched filter (French: _filtre adapté_).
The cross correlation between $f$ and $g$ gives a new image $R_{f,g}$ defined as:

$$
  R_{f,g}(u,v) = \sum_{m,n} f(m,n) g(u+m,v+n).
$$

The cross-correlation can be calculated as a convolution, hence the term "filter" in the name of this technique.

Usually, $f$ and $g$ are normalized into:

$$
  \tilde{f}(m,n) = \frac{ f(m,n)-\mu_f }{ \sigma_f } \qquad
  \tilde{g}(m,n) = \frac{ g(m,n)-\mu_g }{ \sigma_g }
$$

where $\mu_f$ and $\sigma_f$ are respectively the mean and the standard deviation of the image $f$.
This results in the normalized cross-correlation (French: _corrélation croisée normalisée_) which is insensitive to changes in amplitude:

$$
  \tilde{R}_{f,g}(u,v) = \sum_{m,n} \tilde{f}(m,n) \tilde{g}(u+m,v+n).
$$

{numref}`F:detection:matched-filter1` gives an example of matched filter.

```{figure} figs/matched-filter-audir8.svg
---
name: F:detection:matched-filter1
---
Normalized cross-correlation with the pattern shown top-left (the letter G).
```

As seen in {numref}`F:matched-filter2`, the major limit of the matched filter is that it is sensitive to variations in orientation, size, etc.


```{figure} figs/matched-filter-plates.svg
---
name: F:matched-filter2
---
Normalized cross-correlation with the pattern shown top-left (the digit 0).
```

To overcome this limit, one can apply several matched filters, each representative of all the variations of the patterns.
However, this idea is very time-consuming!

<!-- Alternative: find characteristics of objects and perform a classification. -->
