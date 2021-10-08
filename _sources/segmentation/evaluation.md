# How to evaluate a segmentation?

This chapter has introduced the usual methods of segmentation, but there are many more!
No method is the best everywhere: the result depends, among other things, on the image itself.
Consequently, it is interesting to evaluate, for the type of image to process, the quality of the segmentation.
For this, different criteria can be used, defined below.
In addition to the image to be segmented, we also need the expected result, which we call "ground truth" (French: _vérité terrain_).

Imagine that the ground truth and the segmentation are the images in {numref}`F:segmentation:eval:gt-est` (binary segmentation).

```{figure} segmentation-eval-gt-est.png
---
height: 200px
name: F:segmentation:eval:gt-est
---
Ground truth $f^*$ (left) and segmentation $f$ (right).
```

Each image has two areas: the segmented object (shown in white) and the background (in black).
So, we can define four types of zones (cf. {numref}`F:segmentation:eval-zones`):

```{margin}
In French, we talk with _vrai positifs_, _vrai négatifs_, _faux positifs_ and _faux négatifs_.
```

- the true positives (TP) represent the pixels considered as being in the object and being really in the object,
- conversely, the true negatives (TN) are the pixels outside the object both in the segmentation and the ground truth,
- the false positive (FP) are the pixels considered by the segmentation in the object, but which in reality are not part of it,
- finally, the false negative (FN) are the pixels of the object that the segmentation has classified outside.

```{figure} eval-zones.png
---
height: 200px
name: F:segmentation:eval-zones
---
Definition of true positive (TP), false positive (FP), true negative (VN) and false negative (FN).
```

From these four quantities, one or the other of the criteria below can be used.

```{panels}
:column: col-lg-6 col-md-6 col-sm-12 col-xs-12 p-2

Sensibility (_sensibilité_)
^^^
$$
\frac{\text{TP}}{\text{TP}+\text{FN}}
$$

---
  
Specificity (_spécificité_)
^^^
$$
\frac{\text{TN}}{\text{TN}+\text{FP}}
$$

---
  
Dice coefficient (_coefficient de Dice_)
^^^
$$
\frac{2\,\text{TP}}{2\,\text{TP}+\text{FP}+\text{FN}} = \frac{2\,|f\, \cap f\,^*|}{|f\,| + |f\,^*|}
$$

---
  
Jaccard coefficient (_coefficient de Jaccard_)
^^^
$$
\frac{\text{TP}}{\text{TP}+\text{FP}+\text{FN}} = \frac{|f\, \cap f\,^*|}{|f\, \cup f\,^*|}
$$
  
```