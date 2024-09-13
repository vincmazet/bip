(labs:lab1)=
# Lab 1

<!-- En gros, les étus sont arrivés jusqu'aux exos 4/5. Bien sûr, certains sont plus en retard et d'autres plus en avance. -->

After completing each exercise, you can refer to the [correction](labs:cor11).
Furthermore, do not hesitate to ask your colleagues and teachers for additional information
or to discuss specific topics.


<!-- >> En TP (mais aussi parfois en cours) : demander d'afficher systématiquement la colorbar. Cela permet notamment d'éviter de travailler à la fois avec des images en int (0-255) et float (0-1). -->

<!-- >> Profil 3D : utiliser une image plus simple (une somme de gaussienne par exemple) car le profil y est plus clair. -->

<!-- >> Astuce : superposer des points ou une ligne sur une image (en prévision de Harris) (google/stackoverflow...) -->

<!-- >> Astuce : comparer deux images (par ex : skimage.util.compare_images). Cf https://scikit-image.org/docs/dev/auto_examples/applications/plot_image_comparison.html#sphx-glr-auto-examples-applications-plot-image-comparison-py (google/stackoverflow...) -->

<!-- >> 2022-2023 : En TP, demander une conclusion à la fin de chaque séance ou exo, dans le but de leur faire apprendre à synthétiser et de prendre du recul ? Entraîner les étus à la PC et la recherche reproductible : préciser le niveau de détails attendus. -->

<!-- >> Rajouter, pour l'histogramme, quelle transformation est à faire pour passer de l'histo d'une image à un histo particulier ? (constant => égalisation, linéaire, autre...) -->

<!-- Exo supplémentaire : affichage d'une image hyperspectrale.
  L'image hyperspectrale Indian\_pines.mat est de taille $145\times145$ pixels et contient 220 bandes spectrales.
  \item Affichez la dixième bande de l'image.
  \item Créez une composition RVB de l'image et affichez-la.
  Vous pouvez pour cela avoir besoin d'effectuer une moyenne (\syntax{mean})
  et de normaliser les bandes pour forcer leurs intensités à être entre 0 et 1.
  \item Affichez les spectres de quelques pixels, par exemple les pixels (34,106), (47,20) et (91,136).
  Utilisez la fonction \syntax{squeeze} qui permet d'éliminer les dimensions vide d'une matrice 3D.
  L'image hyperspectrale Indian\_pines.mat a été capturée en 1992 par le capteur Aviris
  au dessus de champs dans l'Indiana, États-Unis.
  C'est une image de $145\times145$ pixels et 220 bandes spectrales réparties entre 400 et 2500 nm. -->
  
<!-- Exo supplémentaire : addition de plusieurs images pour constater que le bruit diminue -->

<!-- Exo supplémentaire : représenter l'histogramme d'une image simple 4x4. -->

<!-- Exo supplémentaire : influence du nb de bins -->




## 1 Getting started

[Python](https://www.python.org/) is a very versatile programming language and can especially be used for scientific programming and image processing.
Python's syntax is very similar to Matlab's one.
Before beginning this lab, you may need to know [](python).
If you use your personal computer, beware of the [module version](python:writing-code).
We will use [Jupyter Lab](https://jupyterlab.readthedocs.io/en/latest/index.html), which runs in a web browser, to write programs.
These programs are saved as _notebooks_.


* First, boot your computer on Ubuntu, then open a terminal by typing `terminal` in the main menu or typing `Ctrl` + `Alt` + `T`.

* Start Jupyter by typing in a terminal:
  ```
  jupyter lab
  ```
  or
  ```
  jupyter-lab
  ```

* In Jupyter Lab, open a new Python 3 notebook and rename it from `File` > `Save Notebook As...`.
  A notebook is a file with extension .ipynb.
  
Now you are ready to write a Python program in the notebook.

* In the first cell of the notebook, write
  ```
  40 + 2
  ```
  and type `Shift` + `Return`.
  The code is executed, the result is displayed then a new cell appears below.

* Like any programming language, the code is written using _variables_ and _functions_.
  A _variable_  stores one (or more) values, whether it is numeric or not.
  The name of the variable can contain letters, numbers (except the first character) or underscore.
  Case is important (_i.e._ `a` and `A` are two different variables).
  Type the instructions below in the second cell:
  ```
  year = 2024
  course = "BIP"
  ```
  and type again `Shift` + `Return`.
  Now the value 2023 is stored in the variable `year`
  and the character string "BIP" is stored in the variable `course`.

* Modify the previous cell by adding the following statement:
  ```
  print(f"{course} {year}")
  ```
  `print` is a _function_ and the string in the brackets is an _argument_.
  Here, this argument is a character string.
  The `f` at the beginning of the string means that it is
  a [formatted string](https://he-arc.github.io/livre-python/fstrings/index.html).
  Type `Shift` + `Return` to run again the code.

A notebook is appealing as it is also possible to add text using the [markdown language](https://en.wikipedia.org/wiki/Markdown).

* Select an empty cell, then click on the drop-down list in the toolbar to select _Markdown_.
  Then you can write formatted text.
  Try to write:
  
  ::::{grid} 1
  :gutter: 3
  
  :::{grid-item-card}
  <html><h2 style="margin-top:0ex">New exercise</h2></html>
  
  Write **bold**, _italic_ or equations: $\sqrt{2}$.
  
  :::
  ::::
  
  This can be useful for inserting titles or keeping comments and notes.
  
Verify your code in the [correction](labs:cor11).


## 2 Display a saved image

* Open a new notebook.

* Download the image 4.2.03.tiff
  ([available online](http://sipi.usc.edu/database/database.php?volume=misc&image=10))
  _in the same folder as your notebook_.

* Write in the notebook the following statements to allow the use of the modules
  `skimage.io` and `matplotlib.pyplot`
  which are renamed `io` and `plt`.
  ```
  import skimage.io as io
  import matplotlib.pyplot as plt
  ```
  
  The names `io` and `plt` are conventional names, but you can define other terms.
  
* Load :
  ```
  f = io.imread("4.2.03.tiff")
  ```
  
  and display it:
  
  ```
  plt.imshow(f)
  ```

* What are the dimensions (in pixels) of the image?

The conversion of a color image with pixel values $r$, $g$, $b$ to a grayscale image with pixel intensity $x$ is made through the transformation

$$
  x = 0.2125 \, r + 0.7154 \, g + 0.0721 \, b.
$$

The coefficients have been obtained by psychovisual studies and guarantee that $x\in[0,1]$ if $r,g,b\in[0,1]$.

````{margin}
In `skimage.color.rgb2gray`, `rgb2gray` is a function in the module `skimage.color`.
So, import the module before using the function, as for example:
```
import skimage.color as clr
clr.rgb2gray(...)
```
````

* Convert the color image to grayscale (`skimage.color.rgb2gray`) then display it.

* Print the intensity of the top-left pixel (which is at position $(0,0)$) by typing `g[0,0]`.

* Print the intensities of the five first pixels of the second row by typing `g[1,0:5]`,
  which extract from `g` the pixels at row 1 and columns 0 to 4 (the last index is not reached).

* Print the intensities of all the pixels in the third row by typing `g[2,:]`,
  which extract from `g` the pixels at row 2 and all the columns.

The natural representation of an image is a two-dimensional display where the intensity of the pixels is given by a color.
However, an image can also be seen as a three-dimensional curve, opening the way to new interpretations.

* Extract a row or a column of pixels from the image,
  then display this brightness profile as a signal (`matplotlib.pyplot.plot`).
  Do you manage to find in this profile the different areas of the image?


## 3 Display several images

<!-- beaucoup d'étus n'automatisent pas les choses, c'est-à-dire qu'ils créent à la main la liste avec les noms des images, et qu'il écrivent 4 fois subplot pour les afficher. Comment les forcer à automatiser tout ça ? De plus, plusieurs font un subplots avec  plusieurs ligne et plusieurs colonne, ce qui complique la tâche : donc leur dire de ne faire qu'une ligne de subplots (ou alors d'afficher les images dans des figures différentes). -->

* Open a new notebook.

* Download and unzip <a href="../_static/data/flowers.zip">flowers.zip</a> in the same folder as your notebook.

* Create a list with the name of the images contained in flowers.zip.
  Instead of listing manually the images, you can look for a code on the web, as for example in
  [Stackoverflow](https://stackoverflow.com/questions/57451177/python3-create-list-of-image-in-a-folder).
  
* Print the number of images.

* Define a figure with as many subplots as images with `matplotlib.pyplot.subplots`.

* Dispaly each images in a specific subplot.
  Use an automatic way by using a for loop on the list creater earlier.  


(lab1:synth-image)=
## 4 Create a simple image

An RGB image is encoded in the form of a three-dimensional array:
the first two dimensions are the spatial dimensions of the image, the third corresponds to the bands.

* Create the array corresponding to the RGB image $40 \times 80$ sketched {numref}`F:lab1:synthimage`:
  
  ```{figure} synthimage.png
  ---
  scale: 80%
  name: F:lab1:synthimage
  ---
  A simple image.
  ```
  
  To do this, create first a black image with the correct dimensions
  (`numpy.zeros` generates an array filled with zeros).
  Then assign the desired value to the elements of the matrix, proceeding band by band, by using for example:
  
  ```
  f[m1:m2, n1:n2, b] = x
  ```
  
  This statement assigns the value `x` to the pixels of the band `b` located between the rows `m1` and `m2`$-1$ and the columns `n1` and `n2`$-1$
  (in Python, indices starts at 0).
  
  
## 5 Setting the intensity range

* Display the image <a href="../_static/data/hdfs.tiff">hdfs.tiff</a>, corresponding to a part of the sky in the southern hemisphere.
  You should only observe a single star.

* What is the dynamic of this image (_i.e._ the minimum and maximum values of the intensities)?

* Sketch (on a paper) how would be the histogram of the image.

* Adjust the intensity range with the arguments `vmin` and `vmax` of the function `matplotlib.pyplot.imshow`
  to observe other objects, most of them being galaxies.

* Try another colormap (argument `cmap`).


## 6 Segmentation by histogram thresholding

* Load the image <a href="../_static/data/santamonica.jpg">santamonica.jpg</a> and convert it to grayscale.

* Display its histogram with `matplotlib.pyplot.hist`,
  after having vectorized the image with `numpy.ravel`.
  
* Try different bin number and discuss the result: what do you observe?

* Choose a suitable threshold to segment the image into two classes.
  To perform thresholding, the easiest way is to display the image
  ```
  f > threshold
  ```
  where `f` is the image to threshold and `threshold` is, well... the threshold value.
  
## 7 Contrast enhancement

* Display the image <a href="../_static/data/haze.png">haze.png</a>, after converting it to grayscale.

* Display its histogram.
  You will notice that the image is not very contrasted: what does that imply on the histogram?

* Multiply the image by a positive real: what happens on the image and its histogram?
  Adjust the intensity range of the image to be the same as the original image.

* Perform an histogram equalization (`skimage.exposure.equalize_hist`).
  Do you achieve the exercise goal?
  
  
<!-- Exo supplémentaire : affichage d'une image hyperspectrale.
  L'image hyperspectrale Indian\_pines.mat est de taille $145\times145$ pixels et contient 220 bandes spectrales.
  \item Affichez la dixième bande de l'image.
  \item Créez une composition RVB de l'image et affichez-la.
  Vous pouvez pour cela avoir besoin d'effectuer une moyenne (\syntax{mean})
  et de normaliser les bandes pour forcer leurs intensités à être entre 0 et 1.
  \item Affichez les spectres de quelques pixels, par exemple les pixels (34,106), (47,20) et (91,136).
  Utilisez la fonction \syntax{squeeze} qui permet d'éliminer les dimensions vide d'une matrice 3D.
  L'image hyperspectrale Indian\_pines.mat a été capturée en 1992 par le capteur Aviris
  au dessus de champs dans l'Indiana, États-Unis.
  C'est une image de $145\times145$ pixels et 220 bandes spectrales réparties entre 400 et 2500 nm. -->
  
<!-- Exo supplémentaire : addition de plusieurs images pour constater que le bruit diminue -->

<!-- Exo supplémentaire : représenter l'histogramme d'une image simple 4x4. -->