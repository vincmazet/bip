# Conclusion

This chapter has introduced the common methods of feature detection:
* cross-correlation for detecting perfectly known patterns;
* Canny detector for detecting lines (based on the image gradient);
* Harris detector for detecting corners (based on the intensity variations in the pixel neighborhood);
* Hough transform for detecting lines or circles (by transforming the image into a parameter space).

<!-- Parler aussi de classification (dont réseaux de neurones), qui sont utilisées sur des features -->

<!-- Rajouter ? SIFT, SURF, sur images binaires (cf binary.ipynb, ACP, isomap, analyse discriminante sur une image, HoG, descripteurs de Fourier -->


## References

<!-- To highlight ref: http://jsfiddle.net/davidThomas/NGyVL/ -->

* (B:detection:Canny1986)=
  J. Canny,
  "A Computational Approach To Edge Detection",
  _IEEE Transactions on Pattern Analysis and Machine Intelligence}_, vol. 8, 1986.
  
* (B:detection:Harris1988)=
  C. Harris and M. Stephens
  "A combined corner and edge detector",
  _Alvey Vision Conference_, p. 147-151, 1988.

* (B:detection:Hough1962)=
  P.V.C. Hough,
  "Method and means for recognizing complex patterns",
  US Patent 3,069,654, 1962.
  
* (B:detection:Marr1980)=
  D. Marr and E. Hildreth,
  "Theory of Edge Detection",
  _Proceedings of the Royal Society of London_, vol. 207, 1980.

* (B:detection:Moravec1980)=
  H. Moravec,
  "Obstacle Avoidance and Navigation in the Real World by a Seeing Robot Rover",
  technical report, Carnegie--Mellon University, Robotics Institute, 1980.
 
* (B:detection:Prewitt1970)=
  J.M.S. Prewitt,
  "Object enhancement and extraction",
  _Picture Processing and Psychopictorics_,
  Academic Press, 1970.

* (B:detection:Roberts1965)=
  L.G. Roberts,
  "Machine Perception Of Three-Dimensional Solids",
  _Computer Methods in Image Analysis_,
  IEEE Press, 1965.
  
* (B:detection:Sobel1968)=
  I. Sobel and G. Feldman,
  "A $3\times3$ Isotropic Gradient Operator for Image Processing",
  In _Stanford Artificial Intelligence Project_, 1968.
