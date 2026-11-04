# Conclusion

Image compression consists of reducing the memory size of an image while modifying it as little as possible to maintain a satisfactory quality.
What is "satisfactory" depends on the application: the goal is not the same for a consumer photograph and a medical image.

There are two types of image compression.
Lossless compression (*e.g.* BMP, GIF, PNG...) does not change the image but the compression gain is limited.
On the contrary, lossy compression (*e.g.* JPEG, WEBP, HEIF...) is able to reach a high compression rate but may lose information;
this is why lossy compression should not be used for images with few details, like cartoons or logos.


<!-- :::{seealso} References

* (B:binary:Bloch2005)=
  I. Bloch *et al.*,
  *Le traitement des images*
  ([volume 1](https://perso.telecom-paristech.fr/bloch/ANIM/poly-anim-t1.pdf),
  [volume 2](https://perso.telecom-paristech.fr/bloch/ANIM/poly-anim-t2.pdf)),
  Polycopié du cours ANIM, Télécom-Paris, 2005.

::: -->