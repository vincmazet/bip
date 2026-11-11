(P:registration:features)=
# Feature detection


Image registration requires reference points (features) in the images to determine the transformation to be applied.
Two families of features can be used and have their respective advantages and limitations,
but they can sometimes be advantageously combined.

<!------------------------------------------------------------------------------------------------>

## Intensity-based (iconic) approach

The intensity-based approach, also called iconic approach,
simply uses the pixel intensities of the whole image.
Alternatively, one may also use the pixel intensities of the Fourier transform of the images
(or any other image transformation).

:::{card} 😀 Pros
The main advantage of intensity-based approach is that it is fully automatic.
:::

:::{card} ☹️ Cons
Since all pixels are processed, memory and computational demands can be high.
Furthermore, intensity-based approaches are sensitive to noise and intensity variation between images.
:::

<!------------------------------------------------------------------------------------------------>

## Feature-based (geometric) approach

With feature-based approach, also called geometric approach,
the registration is not defined based on pixel intensities but rather on specific features of the image.
These features can be:
* intrinsic to the image, such as corners, object contours, etc.
* extrinsic to the image, such as markers placed on the objects.

The features are then paired between the two images: this is called feature matching.

:::{figure} figs/feature-matching.svg
:width: 800px
:name: F:registration:feature-based
Feature matching between two remote sensing images.
In this example, intrinsic features (corners) are chosen.
:::

:::{card} 😀 Pros
The advantages of feature-based approach is to use a sparse representation of the image,
thus having a low computational burden.
:::

:::{card} ☹️ Cons
However, feature-based approach has the following limits:
- the matching between features can be difficult,
- the registration accuracy depends on the accuracy of feature extraction,
- the registration accuracy is only guaranteed in the neighborhood of the features.
:::