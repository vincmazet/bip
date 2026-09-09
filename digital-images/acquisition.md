(P:digital-images:acquisition)=
# Image acquisition

<!------------------------------------------------------------------------------------------------>

## Human vision

@F:digital-images:eye shows a simplified cross section of the human eye.

:::{figure} https://upload.wikimedia.org/wikipedia/commons/d/d0/Three_Main_Layers_of_the_Eye.png
:name: F:digital-images:eye
:width: 50%
Simplified diagram of the human eye.
:::

The eye is basically composed of:
* the cornea (French: *cornée*), a transparent tissue that covers the surface of the eye,
* the lens (French: *cristallin*), a second transparent tissue that refracts light onto the retina by changing its shape,
* the retina (French: *rétine*) which lines the inside of the posterior portion of the eye.
  The light from an object is imaged on the retina when the eye is properly focused.

:::{aside}
[A nice video](https://youtu.be/FvbNrwjIrNU).
:::

The human eye's retina contains two kinds of receptors.
The rods (French: *bâtonnets*) provide an overall picture of the field of view and are sensitive to low levels of illumination.
The cones (French: *cônes*) allow color vision.
There are three types of cones which are sensitive to short (S), medium (M) and long (L) wavelength of the visible light (see @F:digital-images:cone-responsivity).
Basically, they are sensitive to blue, green and red light.
Rods and cones are connected to the brain by nerves, which proceeds to the image analysis.

:::{figure} https://upload.wikimedia.org/wikipedia/commons/thumb/0/04/Cone-fundamentals-with-srgb-spectrum.svg/960px-Cone-fundamentals-with-srgb-spectrum.svg.png
:name: F:digital-images:cone-responsivity
:width: 100%
Responsivity of the three kinds of cones, compared to electromagnetic spectrum.
:::

<!------------------------------------------------------------------------------------------------>

## Image acquisition

The principal phenomenon at the origin of the acquisition of an image is the electromagnetic spectrum.
Images based on radiation from the electromagnetic spectrum are the most familiar,
especially images from visible light, as photography.
Other images based on the electromagnetic spectrum include 
radiofrequency (radioastronomy, MRI),
microwaves (radar imaging),
infrared wavelengths (thermography),
X-rays (medical, astronomical or industrial imaging)
and even gamma rays (nuclear medicine, astronomical observations).

In addition to electromagnetic imaging, various other modalities are also employed.
These modalities include
acoustic imaging (by using infrasound in geological exploration or ultrasound for echography),
electron microscopy,
and synthetic (computer-generated) imaging.

::::{dropdown} Examples of image modalities

:::{figure} ../src/figs/interferometry.jpg
:width: 300
Interferometry.
:::

:::{figure} ../src/figs/x-ray.jpg
:width: 300
Radiograph of the right knee.
:::

:::{figure} ../src/figs/thermography.jpg
:width: 300
Thermogram of a passive building, with traditional building in the background.
:::

:::{figure} ../src/figs/MRI.jpg
:width: 300
MRI of the brain (axial section) showing white matter and grey matter folds.
:::

:::{figure} ../src/figs/seismic.jpg
:width: 300
Seismic reflection image.
:::

:::{figure} ../src/figs/electron-microscopy.jpg
:width: 300
Image of pollen grains taken on a electron microscope.
:::

::::

In the following, we focus mainly on electromagnetic imaging, especially through visible light.

<!------------------------------------------------------------------------------------------------>

## Sensor (electromagnetic imaging)

<!-- détailler, en particulier sur les aspects géométriques.
FH propose de rajouter dans BIP : formation des images caméra optique classique (géométrique, photométrique, bruits, il y avait des TP avant sur les caméras rapides, projection perspective, CCD, CMOS. cf avec Adlane par ex), modalité d'imagerie très différentes (impossible de tout couvrir) -->

A [photodiode](https://en.wikipedia.org/wiki/Photodiode) is the most common and basic sensor for image acquisition with visible light.
It is constructed of silicon materials so that its output voltage is proportional to incoming light.

:::{figure} ../src/figs/photodiode.svg
:name: F:digital-images:photodiode
:width: 100
Electronic symbol of a photodiode.
:::

:::{aside}
In addition to this, other systems exist by moving a line of single sensors (as in photocopiers),
by using mirrors, etc.
:::

To acquire a 2D digital image, the typical system involves using a matrix of single sensors.
Two technologies coexist.

* The prevailing technology to read the output voltage of each single sensor is the CMOS
  (complementary metal oxide semi-conductor) approach:
  each single sensor is coupled with its own analog-to-digital conversion circuit.
  This simple counting process makes CMOS technology cheap and low energy.
  However, it may be less sensitive and can produce distortions
  in case of rapid movements in the field of view.

* On the other hand, the CCD (charge coupled device) approach has declined since the 2010s.
  The fundamental idea of the CCD is the use of a unique conversion circuit.
  The potential of each sensor is moved pixel by pixel: the potentials are shifted by one column,
  then those at the last column are counted by a unique circuit.
  CCD is progressively disappearing because of several reasons:
  moving potentials is not instantaneous and consumes energy,
  and it sometimes creates undesirable side effects,
  such as [blooming](https://upload.wikimedia.org/wikipedia/commons/0/01/Blooming_example.jpg).
  
To reproduce human color vision, the acquisition mimics the three kind of cones by using three kind of filters in front of the sensors.
Then, three images are actually acquired, corresponding to the short (blue), medium (green) and long (red) wavelengths.
The Bayer filter (@F:digital-images:bayer-filter) is the widely used technique
for generating color images.
It is a mosaic of red, green and blue filters on a square grid of photosensors.
Note that the filter pattern is half green, one quarter red and one quarter blue.
The reason for having twice green filter than the other colors is because the human vision is naturally more sensitive to green light.

:::{aside}
Rarely, the photodiodes in the sensor matrix are not arranged on a rectangular grid.
For example in astronomy, the sensors can be arranged on an hexagonal grid.
:::

:::{figure} ../src/figs/bayer-filter.svg
:name: F:digital-images:bayer-filter
:width: 70%
The Bayer filter on an image sensor.
:::

<!--
Évoquer dans chaque section les particularités liées aux différents types d'images :
- niveau de gris, multispectral/hyperspectal
- visible, IR ou même non électromagnétique
- tomographie, PET, IRM, scanner
- Computational photography (New cameras do not capture photons;they compute pictures)
  + flutter shutter
- interférométrie
- SKA (utile aussi pour la fabrication d'une image avec un capteur non classique)
- radar
- Example on Acoustic Images
-->

<!------------------------------------------------------------------------------------------------>

## Sampling and quantization

<!-- compressive sensing -->

The final step of digital image formation is digitization,
which is both the sampling and quantization of the observed scene.

### Sampling

Sampling corresponds to mapping a continuous scene onto a discrete grid.
This is naturally done by the matrix of pixels.
Sampling a continuous image leads to a loss of information.
Intuitively, it is clear that sampling reduces resolution and that fine structures will be lost.
Thus the number of pixels on the sensor, directly related to the sampling, is crucial
(see @F:digital-images:aliasing).

:::{figure} figs/square-aliasing.svg
:name: F:digital-images:aliasing
:width: 100%
Images made of black and white squares of different sizes.
The results show significant aliasing for squares of size 0.8 and 0.12 pixels.
Note that the right image looks like a "normal" image.
:::

Besides, distortions also occur when resizing an image with fine structures,
as seen in @F:digital-images:moire.

:::{figure} figs/moire.jpg
:name: F:digital-images:moire
:width: 100%
Me with my favourite moiré shirt.
Left: image of size 1000×1000,
right: image of size 595×595.
:::

This kind of distortion is called aliasing.
It is also called moiré effect in images with pediodic or nearly periodic components.
To avoid aliasing, one has to satisfy the sampling theorem
which states that a continuous scene can be sampled with no error if the sampling intervals are

$$
\Delta x < \frac{T_x}{2}
\quad\text{and}\quad
\Delta y < \frac{T_y}{2}
$$

where $\Delta x$ and $\Delta y$ are the sampling intervals in the two directions (*i.e.* the distance between two consecutive samples)
and $T_x$ and $T_y$ are the periods of the finest structures in the image.

In practice, one prefers to put an optical [low-pass filter](#P:filtering:lowpass) before the sensor
to vanish the high frequencies responsible for aliasing,
that is to increase $T_x$ and $T_y$ such that the sampling theorem is satisfied.


### Quantization

Quantization corresponds to mapping the continuous light intensities to a finite set of numbers.
Typically, image are quantized into 256 gray valuPes; then, each pixel then occupies one byte (8 bits).
The reason for assigning 256 gray values to each pixel is
not only because it is well adapted to the architecture of computers,
but also because it is good enough to give humans
the illusion of a continuous change in gray values.

:::{figure} figs/quantization.png
name: F:digital-images:quantization
width: 100%
Quantization of the same image with (from left to right)
256, 16, 4, and 2 gray levels.
:::

However, quantization naturally introduces errors on the intensities.
If the quantization levels are equally spaced with a distance $d$
and all gray values are equally probable,
the standard deviation of the quantification error is lower than $0.3d$
[[Jähne 2005, p. 243]](#B:digital-images:Jahne2005).
For most common applications, the error is sufficiently low to be acceptable.
But some applications, such as medical imaging or astronomy,
require a finer resolution and, in consequence, use more than 256 gray levels.

<!------------------------------------------------------------------------------------------------>

## Distortions

In addition to the moiré effect and quantization noise,
other distortions can affect the image acquisition.
The two main distortions are noise and blurring.

### Noise

Noise introduces erroneous intensities in the digital image.
Sources of noise are multiple, from electronic noise due to the imaging system itself
to the acquisition conditions (low-light-level for example).
The main noise models are desribed in @C:denoising:noise-sources:
Gaussian noise, Poisson noise and salt-and-pepper noise.
In specific imaging systems, other noise can be encountered.
For example, in radar imaging systems the noise is considered to be multiplicative
and is called speckle noise.

:::{figure} ../src/figs/dark-current.jpg
:width: 400px
:name: F:digital-image:dark-current
Noise on a photograph taken in a dark room (this noise is called "dark current").
:::

### Point spread function

Despite the high quality of an imaging system,
a point in the observed scene is not imaged onto a point in the image space,
but onto a more or less extended area with varying intensities.
The function that describes the imaging of a point is an essential feature of the imaging system and is called the point spread function or PSF (French: *fonction d'étalement du point*).
Generally, the PSF is assumed to be independent of the position.
Then, the imaging system can be treated as a linear shift-invariant system,
which is mathematically described as a convolution (see the [dedicated chapter](P:filtering:convolution)).
Sometimes, an imaging system is described not by its PSF
but by its [Fourier transform](#P:filtering:fourier),
and it is called optical transfer function, or OTF (French: *fonction de transfert optique*).

:::{figure} ../src/figs/budapest.jpg
:width: 400px
:name: F:digital-image:example-motion
Example of blur (parliament of Budapest).
:::