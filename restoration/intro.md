(P:restoration:intro)=
# Restoration


Restoration methods (French: *méthodes de restauration*) aim to improve an image by using methods based on objective considerations.
Conversely, enhancement methods previously covered (*e.g.* @P:digital-images:histogram-transformations)
rely mostly on heuristic procedures designed to improve the visual appearance of an image, that is, "to look visually fine".

Restoration methods need knowledge of the phenomenon that has degraded the image.
This knowledge gives a mathematical model of the degradation.
This degradation is then "inverted" to recover the original image:
hence restoration methods are formulated as an *inverse problem* (French: *problème inverse*): see @F:restoration:inverse-problem.
This approach typically defines a *criterion of goodness* (French: *critère de qualité*):
this is a mathematical function whose minimum corresponds to the best possible restoration.

:::{figure} figs/inverse-problem.png
:width: 100%
:name: F:restoration:inverse-problem
Direct and inverse problems.
:::

<!-- donner des exemples réels, liés à des problèmes de restauration (denoising, deconvolution, dehazing, gestion des distortions) ? -->
