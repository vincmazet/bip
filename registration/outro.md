(P:registration:outro)=
# Conclusion

Image registration is the process of aligning images into a common reference frame, with the goal of comparing or combining their respective information.

The pipeline of image registration is illustrated @F:registration:bigpicture.
In this example, the goal of registration is to find the transformation to apply to the source image $f$ so that the registered (transformed) image $f'$
is similar to a reference image $g$.

:::{figure} figs/bigpicture.png
:width: 100%
:name: F:registration:bigpicture-outro
Image registration.
:::

Registration usually decomposes into three steps (@F:registration:bigpicture-outro):
- choosing the features on which matching will be computed,
- selecting a deformation model depending on the transformation between the two images (classified into two families: linear and non-linear),
- defining a similarity metric and optimizing it to obtain the best parameters of the transformation.
