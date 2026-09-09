(C:formation)=
# Formation of images


## Human vision

{numref}`F:digital-images:eye` shows a simplified cross section of the human eye.

```{figure} https://upload.wikimedia.org/wikipedia/commons/d/d0/Three_Main_Layers_of_the_Eye.png
---
name: F:digital-images:eye
width: 80%
---
Simplified diagram of the human eye.
```

The eye is basically composed of:
* the cornea (french: _cornée_), a transparent tissue that covers the surface of the eye,
* the lens (french: _cristallin_), a second transparent tissue that refract light on the retina by changing shape,
* the retina (french: _rétine_) which lines the inside of the posterior portion of the eye.
  The light of an object is imaged on the retina when the eye is properly focused.

```{margin}
[A nice video](https://youtu.be/FvbNrwjIrNU).
```

The retina of human eye contains two kinds of receptors.
The rods (french: _bâtonnets_) give an overall picture of the field of view and are sensitive to very low levels of illumination.
Besides, the cones (french: _cônes_) allow color vision.
There are three types of cones which are sensitive to short (S), medium (M) and longer (M) wavelength of the visible light (see {numref}`F:digital-images:cone-responsivity`).
Basically, they are sensitive to blue, green and red light.
Rods and cones are connected by nerves to the brain, which proceeds to the image analysis.

```{figure} https://upload.wikimedia.org/wikipedia/commons/0/04/Cone-fundamentals-with-srgb-spectrum.svg
---
name: F:digital-images:cone-responsivity
---
Responsivity of the three kinds of cones, compared to electromagnetic spectrum.
```


## Image acquisition

[Photodiode](https://en.wikipedia.org/wiki/Photodiode) is the most common and basic sensor for image acquisition.
It is contructed of silicon materials so that its output voltage is proportional to incoming light.
The use of a colored filter in front of the photodiode improves selectivity.

To acquire a 2D digital image, the usual system is by using a matrix of single sensors,
but other systems exists by moving a line of single sensors (as in photocopiers), by using mirrors, etc.
The prevailing technology to read the output voltage of each single sensor is the CMOS approach:
each single sensor is coupling with its own analog-to-digital conversion circuit.
This simple counting process makes the CMOS technology cheap and low energy.
However, it may be less sensitive and may produce distortion in case of rapid movings in the filed of view.

On the other hand, the CCD (charge coupled device) approach has narrowed since the 2010s.
The fundamental idea of the CCD is the use of a unique conversion circuit.
The potential of each sensor is moved pixel by pixel: the potentials are shifted by one column, then those at the last column are counted by the unique circuit.
But moving potentials is not instantaneous and consumes energy.
Besides, it sometimes creates undesirable side effects (e.g. [blooming](https://upload.wikimedia.org/wikipedia/commons/0/01/Blooming_example.jpg)).
as possible on the sensitive area. 



PSF de l'instrument

type d'images :
- niveau de gris, multispectral/hyperspectal
- visible, IR ou même non électromagnétique
- tomographie, PET, IRM, scanner
- Computational photography (New cameras do not capture photons;they compute pictures) : flutter shutter
- interférométrie
- SKA (utile aussi pour la fabrication d'une image avec un capteur non classique)
- radar
- Example on Acoustic Images

Image sampling ad quantization
- basic concepts in sampling and quantization
- quantification, bruit de quantification
- échantillonnage, moiré, compressive sensing
- Image acquisition : sampling, quantification, interpolation, psf, pyramids
- grille non régulière, voisinage, connexité

- Sensor and noise : Gaussian noise, multivariate data, speckle noise, bruit multiplicatif


## Representing digital images

technologie des écrans
spatial and intensity resolution
écrans (pixel, luminophore) + synthèse additive, soustractive
Espaces couleurs : RGB, HSV, CMY(K), ...
évoquer l'interpolation
- Image formats, compressé et non compressé, vectoriel et matriciel



