(P:registration:intro)=
# Registration

:::{caution}
This chapter is currently being written and will be ready in a few days.
:::


Image registration is the process of applying geometric transformation on images so that they lie in the same coordinate system.
Registration has many applications, for instance in remote sensing ({numref}`F:registration:application:remote-sensing`),
medical imaging ({numref}`F:registration:application:medical`),
or photograph stitching ({numref}`F:registration:application:stitching`).

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

```{figure} XXX/vincent13.png
---
width: 400px
name: F:registration:application:stitching
---
Photograph stitching.
```

Exemples
- Intra-individual monomodal registration :
  - One patient, two exams n-months appart (Estimate a transformation (in this case rigid) to compensate for the difference in positioning of the patient in the camera.)
  - Dynamic lung imaging : Requires a deformable registration to compensate for the patient’s respiratory movements.
  - Estimate a rigid or affine transformation to superimpose the informations and take advantage of the complementary nature of these two imaging techniques.
  - Requires deformable alignment to compensate for movements related to breathing, the placement of organs in the abdomen, etc.
- Inter-individual registration

Several scenarios
* Monomodal vs multimodal registration
* Registration of 2D/2D, 2D/3D, 3D/3D, 3D+t, nD/nD images
•   Global  vs  local   /   rigid   vs  deformable  transforma6on













The pipeline of image registration is given in {numref}`F:registration:bigpicture`.
The next sections are devoted to give details on each step.

```{figure} XXX/bigpicture.png
---
width: 100%
name: F:registration:bigpicture
---
Image registration.
In this example, the characteristics are the edges, but they can be other informations like keypoints.
```









The majority of the registration methods consists of the following four steps (see Fig. 1):
* Feature detection. Salient and distinctive objects (closed-boundary regions, edges, contours, line intersections, corners, etc.)
  are manually or, preferably, automatically detected. For further processing, these features can be represented by their point representatives
  (centers of gravity, line endings, distinctive points), which are called control points (CPs) in the literature.
* Feature matching. In this step, the correspondence between the features detected in the sensed image and those detected in the reference image is established.
  Various feature descriptors and similarity measures along with spatial relationships among the features are used for that purpose.

* Transform model estimation. The type and parameters of the so-called mapping functions, aligning the sensed image with the reference image, are estimated.
  The parameters of the mapping functions are computed by means of the established feature correspondence.
  + Image resampling and transformation. The sensed image is transformed by means of the mapping functions.
  Image values in non-integer coordinates are computed by the appropriate interpolation technique. 
