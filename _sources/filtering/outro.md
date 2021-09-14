# Conclusion

Filtering consists in amplifying or attenuating some frequencies in an image.
It is used sometimes for image processing,
and this is what happens when an image is acquired.
Indeed, a blurred photo is a (low-pass) filtered version of the actual scene.

In this chapter, we have seen two mathematical objects used to filter images and analyze their properties.
The first one is convolution which is the mathematical operation used to compute the result of filtering in the usual spatial domain.
The second one is the Fourier transform which gives the representation of an image in the frequency domain.
So, the operation of filtering comes to multiplication in this domain.
Besides, the Fourier transform is used to analyze the frequency content of an image,
as we will see in [](denoising) and [](deconvolution).

A question remains: is there an inverse convolution operator, like division is the inverse of multiplication?
The answer is generally no.
Practically, the quantification in the image, the presence of noise and the lack of knowledge of the PSF make the problem hard,
justifying a [specific section](deconvolution) to deal with.



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