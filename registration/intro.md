(P:registration:intro)=
# Registration

:::{caution}
This chapter is currently being written and will be ready in a few days.
:::

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

:::{figure} figs/bigpicture.png
:width: 100%
:name: F:registration:bigpicture
Image registration
(in this example, the features chosen for registration are the edges, but others can be used).
:::

Most registration methods consist of the following three steps,
which are highlighted by the blue regions in @F:registration:bigpicture and detailed in the next sections:
- @P:registration:features: distinctive objects within the images (*e.g.* edges or corners) are identified;
- @P:registration:metrics: correspondences between the features detected in the two images are established;
- @P:registration:deformation: a transformation of the source image is computed to align it with the reference image.
  The parameters of the transformation are those that minimize the similarity criterion.
  An interpolation of the source image is performed to generate the registered image.