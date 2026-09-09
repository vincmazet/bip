# Conclusion

We have seen that segmentation consists in dividing an image into several homogeneous regions.
The homogeneity of a region is based on color, texture, contours, etc.

The methods of segmentation are very diverse, and we have only seen a few of them.
Other existing methods include active contours or the so-called snakes, level sets, Markovian models, etc.
In addition to these "model-based" methods, deep learning allows significant increases in the results.

At last, we list some criteria to evaluate the quality of a segmentation method.
These criteria are useful to compare different segmentation methods, as presented in [](labs:lab4).

## References

* (B:segmentation:MacQueen1967)=
  J.B. MacQueen,
  "Some Methods for classification and Analysis of Multivariate Observations",
  _Proceedings of 5th Berkeley Symposium on Mathematical Statistics and Probability_,
  vol. 1, p. 281--297, 1967

* (B:segmentation:Otsu1979)=
  N. Otsu,
  "A threshold selection method from gray-level histograms",
  _IEEE Transactions on Systems, Man, and Cybernetics_,
  vol. 9, no 1, p. 62-66, 1979.

* (B:segmentation:Steinhaus1957)=
  H. Steinhaus,
  "Sur la division des corps matériels en parties",
  _Bull. Acad. Polon. Sci._,
  vol. 4, no 12, p. 801-804, 1957.

<!--
 
Autres méthodes :
- par texture
- Mean-shift {Fukunaga75}
- SLIC {Achanta12}
- Split/merge
- Snakes
- Deep learning (maintenant il n'y a plus que ça !)

  \bibitem[Achanta  et coll. 2012]{Achanta12}
  R. Achanta, A. Shaji, K. Smith, A. Lucchi, P. Fua, S. Süsstrunk,
  \og{}SLIC Superpixels Compared to State-of-the-art Superpixel Methods \fg{},
  \emph{IEEE Transactions on Pattern Analysis and Machine Intelligence}, 34(11), p. 2274--2282, 2012.

  \bibitem[Fukunaga \& Hostetler 1975]{Fukunaga75}
  K. Fukunaga, L.D. Hostetler,
  \og{}The Estimation of the Gradient of a Density Function, with Applications in Pattern Recognition\fg{},
  \emph{IEEE Transactions on Information Theory}, 21(1) p. 32--40, 1975.

  \bibitem[MacQueen 1967]{MacQueen67}
  J.B. MacQueen,
  \og{}Some Methods for classification and Analysis of Multivariate Observations\fg{},
  5th Berkeley Symposium on Mathematical Statistics and Probability., p. 281--297, 1967.

  \bibitem[Otsu 1979]{Otsu79}
  N. Otsu,
  \og{}A threshold selection method from gray-level histograms\fg{},
  \emph{ IEEE Transactions on Systems, Man, and Cybernetics} 9(1) p. 62--66, 1979.

  \bibitem[Sezguin et Sankur 2004]{Sezgin04}
  M. Sezgin, B. Sankur,
  \og{}Survey over image thresholding techniques and quantitative performance evaluation\fg{},
  \emph{Journal of Electronic Imaging} 13(1), p. 146--165, 2004.

  \bibitem[Steinhaus 1957]{Steinhaus57}
  H. Steinhaus,
  \og{}Sur la division des corps matériels en parties\fg{}
  \emph{Bulletin de l'Académie Polonaise des Sciences}, 4(12) p. 801--804, 1957.
 -->
