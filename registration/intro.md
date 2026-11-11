(P:registration:intro)=
# Registration

Image registration is the process of applying geometric transformations on images so that they lie in the same coordinate system.
Registration has many applications, for instance in
remote sensing (@F:registration:application:remote-sensing),
medical imaging (@F:registration:application:medical),
or photograph stitching (@F:registration:application:stitching).

```{figure} XXX/vincent4.png
---
width: 400px
name: F:registration:application:remote-sensing
---
Registration of remote sensing images.
```

```{figure} XXX/vincent6.png
---
width: 400px
name: F:registration:application:medical
---
Change detection in medical imaging.
```

<!-- Intra-individual monomodal registration :
  - One patient, two exams n-months appart (Estimate a transformation (in this case rigid) to compensate for the difference in positioning of the patient in the camera.) -->

```{figure} XXX/vincent13.png
---
width: 400px
name: F:registration:application:stitching
---
Photograph stitching.
```

The pipeline of image registration is illustrated @F:registration:bigpicture.
In this example, the goal of registration is to find the transformation to apply on the source image $f$ so that the registered (transformed) image $f'$
is similar to a reference $g$.

:::{figure} figs/bigpicture.png
:width: 100%
:name: F:registration:bigpicture
Image registration.
:::

Most registration methods consist of the following three steps,
which are highlighted by the blue regions in @F:registration:bigpicture and detailed in the next sections.
- @P:registration:features: distinctive objects (*e.g.* edges or corners) are identified in the reference and source images.
  For example, the chosen features in @F:registration:bigpicture are the edges.
- @P:registration:deformation: the transformation of the source image is defined by its type and parameters,
with the optimal parameters determined by minimizing the similarity metric.
An interpolation of the source image is then performed to generate the registered image.
- @P:registration:metric: a correspondence between the features detected in the two images are established.
  The lower the similarity metric, the better the registration.