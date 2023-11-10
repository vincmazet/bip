# Introduction

The principal goal of restoration methods (French: _méthodes de restauration_)
is to improve an image by using methods based on objective considerations.
On the contrary, enhancement methods that we have seen (_e.g._ in [](C:histogram-transformations))
are mostly heuristic procedures designed to improve an image for a psychophysical purpose,
that is, "to look visually fine".

Restoration methods need knowledge of the phenomenon that has degraded the image.
This knowledge gives a mathematical model of the degradation.
The degradation phenomenon is "inversed" to recover the original image:
hence restoration methods are said to be an _inverse problem_ (French: _problème inverse_).
This approach usually involves formulating a _criterion of goodness_ (French: _critère de qualité_) to help the search for an optimal estimation:
a criterion is a mathematical function whose minimum corresponds to the best possible restoration.


<!-- introduire le schéma : x -> dégradation -> y -> restauration -> \hat{x} -->
<!-- donner des exemples réels, liés à des problèmes de restauration (denoising, deconvolution, dehazing, gestion des distortions -->

<!-- on ne voit pas l'aspect knowledge et model et inversion dans certains filtres de débruitage -->