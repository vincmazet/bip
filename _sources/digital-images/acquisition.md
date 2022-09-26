(C:digital-images:acquisition)=
# Image acquisition

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

The principal phenomenon at the origin of the acquisition of an image is electromagnetic spectrum.
Images based on radiation from the electromagnetic spectrum are the most familiar,
especially images from visible light, as photography.
Other images from electromagnetic spectrum are based on
radiofrequency (radioastronomy, MRI),
microwaves (radar imaging),
infrared wavelengths (thermography),
X-rays (medical, astronomical or industrial imaging)
or even gamma rays (nuclear medicine, astronomical observations).

In addition to electromagnetic imaging, there are a number of other modalities that are also used,
such that
acoustic imaging (by using infrasound in geological exploration or ultrasound for echography),
electron microscopy,
or even synthetic (computer-generated) imaging.



````{dropdown} Examples of image modalities

```{figure} interferometry.jpg
---
width: 300
---
Interferometry.
```

```{figure} x-ray.jpg
---
width: 300
---
Radiograph of the right knee.
```

```{figure} thermography.jpg
---
width: 300
---
Thermogram of a Passivhaus building, with traditional building in background.
```

```{figure} MRI.jpg
---
width: 300
---
MRI of the brain (axial section) showing white matter and grey matter folds.
```

```{figure} seismic.jpg
---
width: 300
---
Seismic reflection image.
```

```{figure} electron-microscopy.jpg
---
width: 300
---
Image of pollen grains taken on a electron microscope.
```


````




In the sequel, we focus on electromagnetic imaging.


## Sensor

[Photodiode](https://en.wikipedia.org/wiki/Photodiode) is the most common and basic sensor for image acquisition.
It is contructed of silicon materials so that its output voltage is proportional to incoming light.

```{figure} photodiode.svg
---
name: F:digital-images:photodiode
width: 100
---
Electronic symbol of a photodiode.
```

```{margin}
In addition to this, other systems exists by moving a line of single sensors (as in photocopiers),
by using mirrors, etc.
```

To acquire a 2D digital image, the usual system is by using a matrix of single sensors.
Two technologies coexist.

* The prevailing technology to read the output voltage of each single sensor is the CMOS
  (complementary metal oxide semi-conductor) approach:
  each single sensor is coupling with its own analog-to-digital conversion circuit.
  This simple counting process makes the CMOS technology cheap and low energy.
  However, it may be less sensitive and may produce distortions
  in case of rapid movings in the field of view.
  
  <!-- illustration du CMOS -->

* On the other hand, the CCD (charge coupled device) approach has narrowed since the 2010s.
  The fundamental idea of the CCD is the use of a unique conversion circuit.
  The potential of each sensor is moved pixel by pixel: the potentials are shifted by one column,
  then those at the last column are counted by a unique circuit.
  CCD progressively disapears because of several reasons:
  moving potentials is not instantaneous and consumes energy,
  and it sometimes creates undesirable side effects
  (e.g. [blooming](https://upload.wikimedia.org/wikipedia/commons/0/01/Blooming_example.jpg)).
  
  <!-- illustration du CCD -->
  
<!-- In some applications, the photodiodes in the sensor matrix are not arranged on a rectangular grid -->

A color or multispectral image ($B>1$) is made of as many grayscale image as bands.
Therefore, to acquire a traditional RGB image, three grayscale images are acquired,
each in a differente wavelength.
The Bayer filter ({numref}`F:digital-images:bayer-filter`) is the widespread technique to generate color images.
It is a mosaic of red, green and blue filters on a square grid of photosensors.
Note that the filter pattern is half green, one quarter red and one quarter blue.
The reason of having twice green filter than the other colors is to mimic the human vision
which is naturally more sensitive to green light.

```{figure} bayer-filter.svg
---
name: F:digital-images:bayer-filter
width: 70%
---
The Bayer filter on an image sensor.
```


## Sampling and quantization

<!-- compressive sensing -->

The final step of digital image formation is digitization,
which is both the samling and quantization of the observed scene.

### Sampling

Sampling corresponds to mapping a continuous scene to a discrete map.
This is naturally done by the matrix of pixels.
Sampling a continuous image leads to a loss of information.
Intuitively, it is clear that sampling leads to a reduction in resolution:
structures of about the scale of the sampling distance and finer will be lost.
Thus the number of pixels on the sensor, which is directly linked to the sampling, is crucial.
Besides, considerable distortions occur when sampling an image with fine structures,
as seen in {numref}`F:digital-images:moire`.

```{figure} moire.jpg
---
name: F:digital-images:moire
width: 100%
---
Me with my favourite moiré shirt.
Left: image of size 1000×1000,
right: image of size 595×595.
```

This kind of distortion is called the moiré effect.
The same phenomenon exists in signal processing and is called aliasing.
To avoid the moiré effect, one has to satisfy the sampling theorem
which imposes a maximal sampling step in function of the frequencies in the image.
In practice, one prefer to put an optical low-pass filter before the sensor
to vanish the high frequencies responsible of the moiré effect.


### Quantization

Quantization correspond to mapping the continuous light intensities to a finite set of number.
Generally, image are quantized into 256 gray values; then, each pixel occupies one byte (8 bits).
The reason for assigning 256 gray values to each pixel is
not only because it is well adapted to the architecture of computers,
but also because the number of values is good enough to give humans
the illusion of a continuous change in gray values.

```{figure} quantization.png
---
name: F:digital-images:quantization
width: 100%
---
Quantization of the same image with (from left to right)
256, 16, 4, and 2 gray levels.
```

Yet, quantization naturally introduces errors on the intensities.
If the quantization levels are equally spaced with a distance $d$
and all gray valeurs are equally probable,
the standard deviation of the quantification error is lower than $0.3d$
[[Jähne 1997, p.220]](B:digital-images:Jahne1997).
For common needs, the error is sufficiently low to be acceptable.
But some applications, like medical imaging or astronomy,
need a finer resolution and, in consequence, use more than 256 gray levels.


## Distortions

In addition to moiré effect and quantization noise,
other distortions can affect the image acquisition.
The two main distortions are noise and blurring.

### Noise

Noise introduces false intensities in the digital image.
Sources of noise are multiple, from electronic noise due to the imaging system itself
to the acquisition conditions (low-light-level for example).
The main noise model are desribed in [denoising:noise-sources]:
Gaussian noise, Poisson noise and salt-and-pepper noise.
In specific imaging systems, other noise can be encountered.
For example, in radar imaging systems the noise is considered to be multiplicative
and is called speckle noise.

```{figure} dark-current.jpg
---
width: 400px
name: F:digital-image:dark-current
---
Noise on a photograph taken in a dark room (this noise is called ``dark current'').
```

<!-- dark current -->

### Point spread function

Despite the high quality of an imaging system,
a point in the observed scene is not imaged onto a point in the image space,
but onto a more or less extended area with varying intensities.
The function that describes the imaging of a point is an essential feature of the imaging system and is called the point spread function or PSF (in French: _fonction d'étalement du point_).
Generally, the PSF is assuming to be independent of the position.
Then, the imaging system can be treated as a linear shift-invariant system,
which is mathematically described as a convolution (see the [dedicated chapter](filtering:convolution)).
Sometimes, an imaging system is not described by its PSF but rather by its
[Fourier transform](filtering:fourier),
and it is called optical transfer function, or OTF (in French: _fonction de transfert optique_).

```{figure} budapest.jpg
---
width: 400px
name: F:digital-image:example-motion
---
Example of blur (parliament of Budapest shoot by a camera).
```