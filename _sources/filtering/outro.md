# Outro


<!-- # Existe-t-il un opérateur inverse de la convolution~? 
* Ce problème est appelé déconvolution.
* Si la PSF est connue et vérifie certaines conditions très particulières (cf. analyse de Fourier)~: c'est possible~!
* En pratique, la quantification et le bruit rendent la déconvolution difficile.

Jähne, p.119
Cette question est importante car des dégradations comme le flou de bougé ou de mauvaise mise au point
peuvent être modélisées par une convolution.
Si un opérateur inverse existe et si la PSF est connue, alors il est possible de reconstruire l'image d'origine.
Le problème de l'inversion d'un filtre est appelé déconvolution ou filtrage inverse.
L'analyse de Fourier montrera que la reconstruction est possible pour des PSF très particulières.
Dans la pratique, la quantification et le bruit rendent la déconvolution encore plus difficile.
-->


Conclusion (FILTERING)

The operation of filtering consists in selecting some frequencies in the images.
Especially, we distinguish low-pass filtering which preserves only the low frequencies ({numref}`F:fourier:lowpass`)
and high-pass filtering which preserves only the high frequencies ({numref}`F:fourier:highpass`).

```{glue:figure} G:fourier:lowpass
:name: "F:fourier:lowpass"

Example of low-pass filtering: only the low frequencies are kept.
Top row: spatial domain, bottom row: amplitude of the DFT.
```

```{glue:figure} G:fourier:highpass
:name: "F:fourier:highpass"

Example of high-pass filtering: only the high frequencies (i.e. the sudden changes in the intensities) are kept.
```
