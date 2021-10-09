(lab4)=
# Lab 4

Three methods will be compared to segment the coins on the image <a href="../_static/data/observation.png">observation.png</a>:
binary thresholding, Otsu's method, and local thresholding.
The methods will be evaluated through the Dice coefficient,
by using the ground truth available in image <a href="../_static/data/groundtruth.png">groundtruth.png</a>.

* Apply binary thresholding to the image, by choosing manually the threshold value.
  Compute the Dice coefficient.
  
  ```{note}
  Dice coefficient is also known as Sørensen–Dice coefficient or Dice similarity coefficient.
  Besides, a Dice _dissimilarity_ coefficient also exists: it is equals to $1-d$ where $d$ is the Dice _similarity_ coefficient.
  
  The function `scipy.spatial.distance.dice` computes the Dice _dissimilarity_ coefficient.
  Also, it works on boolean 1D arrays, not or 2D arrays.
  Recall that `A.ravel()` returns a vectorized version of the array `A` (see `numpy.ndarray.ravel`).
  Besides, `A.astype(bool)` returns a boolean version of the array `A` (see `numpy.ndarray.astype`).
  ```

* Use `skimage.filters.threshold_otsu` to get a threshold value by Otsu's method and apply the thresholding.
  Compute the Dice coefficient.
  What differences do you observe between the two first segmentations? How can these differences be explained?

* Use `skimage.filters.threshold_local` to perform local thresholding.
  How works this method?
  Compute the Dice coefficient.
  
* Finally, criticize the three methods: identify the good results and the limitations.
  Suggest improvements.