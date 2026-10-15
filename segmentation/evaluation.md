# How to evaluate a segmentation?


This chapter has introduced the usual methods of segmentation, but there are many more!
No method is the best because the result depends, among other things, on the image itself.
Consequently, it is interesting to have an objective evaluation of the segmentation quality.
To do that, different criteria can be used, defined below.
In addition to the image to be segmented, we also need the expected result, which we call "ground truth" (French: *vérité terrain*).

Imagine that the ground truth and the segmentation are the images in @F:segmentation:eval:gt-est, in the case of a binary segmentation.

:::{figure} figs/segmentation-eval-gt-est.png
:height: 200px
:name: F:segmentation:eval:gt-est
Ground truth $f^*$ (left) and segmentation $f$ (right).
:::

Each image has two areas: the segmented object (shown in white) and the background (in black).
So, we can define four types of zones (cf. @F:segmentation:eval-zones):

:::{margin}
In French, we talk with *vrai positifs*, *vrai négatifs*, *faux positifs* and *faux négatifs*.
:::

- the true positives (TP) represent the pixels considered as being in the object and being really in the object,
- conversely, the true negatives (TN) are the pixels outside the object both in the segmentation and the ground truth,
- the false positive (FP) are the pixels considered by the segmentation in the object, but which in reality are not part of it,
- finally, the false negative (FN) are the pixels of the object that the segmentation has classified outside.

:::{figure} figs/eval-zones.png
:height: 200px
:name: F:segmentation:eval-zones
Definition of true positive (TP), false positive (FP), true negative (VN) and false negative (FN).
:::

From these four quantities, several criteria can be defined,
below are the most usual ones.
The variables $f^*$ and $f$ are the ground truth and the segmentation
and are considered as sets from which one can compute their cardinality (denoted $|\cdot|$).

::::{grid} 1 1 2 2

:::{card} Sensibility (*sensibilité*) or Recall
$$
\frac{\text{TP}}{\text{TP}+\text{FN}}
$$
:::

:::{card} Specificity (*spécificité*)
$$
\frac{\text{TN}}{\text{TN}+\text{FP}}
$$
:::

:::{card} Precision (*précision*)
$$
\frac{\text{TP}}{\text{TP}+\text{FP}}
$$
:::

:::{card} Dice coefficient (*coefficient de Dice*) or F1 score
$$
\frac{2\,\text{TP}}{2\,\text{TP}+\text{FP}+\text{FN}} = \frac{2|f \cap f^*|}{|f| + |f^*|}
$$
:::

:::{card} Jaccard coefficient (*coefficient de Jaccard*)
$$
\frac{\text{TP}}{\text{TP}+\text{FP}+\text{FN}} = \frac{|f \cap f^*|}{|f \cup f^*|}
$$
:::

:::{card} Accuracy (*exactitude*)
$$
\frac{\text{TP}+\text{TN}}{\text{TP}+\text{FP}+\text{TN}+\text{FN}}
$$
:::

::::