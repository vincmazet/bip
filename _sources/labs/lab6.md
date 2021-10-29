(lab6)=
# Lab 6


This lab is devoted to metrology, by detecting features on the image <a href="../_static/data/L.png">L.png</a>.

* Recall what the following detectors can do: Canny, Harris, Hough, Moravec, Prewitt, Roberts, Sobel.
  

## Sobel and Canny detectors

* Display the image gradients with the Sobel detector (`skimage.filters.sobel`).

* Apply a threshold on the obtained image to perform an edge detection.
  What is the influence of the threshold on the result?

* Find the optimal threshold, _i.e._ the one which gives most of the edges of the object while keeping precise locations of the edges.

* What is the relationship between Sobel and Canny detectors?

* Display the edges detected by Canny detector (`skimage.feature.canny`).

* Discuss the influence of the main parameters of the method,
  namely the size of the Gaussian filter and the two thresholds.

* It is sometimes interesting to compare the studied methods in terms of computation time.
  The computation time can be obtained by calculating the difference
  between the time $t_2$ measured after executing the method and the time $t_1$ measured before its execution.
  For that, you can use the function `time.time` which gives the number of seconds elapsed since January 1, 1970.
  What is the fastest method?
  

## Harris detector

* Apply the Harris detector (with `skimage.feature.corner_harris` and `skimage.feature.corner_peaks`).

* Criticize the result: have all the corners been detected?
  Are there any false alarms (_i.e._ detections that do not correspond to corners)?
  How to explain these errors?
  

## Hough transform

* The Hough transform does not apply directly to the original image: what image should you use?

* Represent the Hough transform of the image with `skimage.transform.hough_line`.

* The function `skimage.transform.hough_line_peaks` extracts the parameters of the most important lines from the Hough transform.
  Use this function to display the six most important lines of the image.


<!-- exo très long pour les étus (bceaucoup de réglages de params) -->
<!-- montrer l'influence des paramètres de chaque fonction -->