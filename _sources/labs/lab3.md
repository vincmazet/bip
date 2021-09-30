(labs:lab3)=
# Lab 3


## Mathematical Morphology

We want to detect and count the number of swimming pools visible in the satellite image <a href="../_static/data/moliets.png">moliets.png</a>.
Most of the functions to use are in module `skimage.morphology`.

```{note}
At first, do not try to find all the pools perfectly:
implement a first version of the method which gives an approximate result automatically.
```

* Apply a threshold on the image to highlight the pools.
  Ask yourself about which image to use: the original image, the grayscale image, a particular band something else?

* Apply the four usual morphological operators (erosion, dilation, opening, closing)
  to observe their influence and deduce the one most suited to the problem.

* By using appropriate measures, classify the regions given in the image to determine the number of pools.

* Determine the surface of the pools, knowing that the image is of resolution 50 cm.

* Give a critical discussion about your method by listing its good behaviours and its limits,
  then suggest improvements.

  
<!-- ## Registration

Two satellite images of the Capitol in Toulouse are to be registered by using an iconic approach:
<a href="../_static/data/capitole1.jpg">capitole1.jpg</a> (the reference) and
<a href="../_static/data/capitole2.jpg">capitole2.jpg</a> (the source).

* Which deformation model is adapted to the problem?

* Before applying a complete registration processing on the two images,
  we first apply an arbitrary distortion to the source.
  To do this, use the appropriate function of the module `skimage.transform`
  to define an Euclidean transformation of translation $(400,-100)$ and of rotation $\pi/3$.
  These parameters are close to the optimal transformation.
  Then apply this transformation on the source with `skimage.transform.warp`.
  Check that the distorted image is close enough to the reference (you can display the difference between the two images).
  
* Implement an optimization method to automatically determine the best parameters of the transformation.
  The simplest optimization method (although very long in computing time!)
  consists of using loops to test several values and keep those that minimize the mean squared error
  (defined in [](labs:lab2)). -->