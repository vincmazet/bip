# Conclusion


Mathematical morphology gathers operators that work on the form of objects.
We have studied some operators applied to binary images, but there are extensions of these techniques to grayscale images.
The results given by the four main operators on binary images are listed in the following table.

````{list-table}
:header-rows: 0
:widths: 10 30

* - ```{image} greece.png
    ```
  - **Original image**

* - ```{image} greece-dilation.png
    ```
  - **Dilation** $\oplus$
    * increases the size of objects (_e.g._ the islands are bigger)
    * fills the small holes (_e.g._ the [Gulf of Corinth](https://en.wikipedia.org/wiki/Gulf_of_Corinth) does not more exist after dilation)
    * welds close objects (_e.g._ some islands are grouped into a larger island)

* - ```{image} greece-erosion.png
    ```
  - **Erosion** $\ominus$
    * decreases the size of objects (_e.g._ Crete is smaller)
    * widens the holes (_e.g._ the Gulf of Corinth is bigger)
    * separates the connected objects by a small bridge (_e.g._ the Peloponnese and mainland Greece are now disconnected)
    * removes small items (_e.g._ small islands have disappeared)

* - ```{image} greece-opening.png
    ```
  - **Opening** $\circ$
    * conserve the size of the objects (while they can be slightly distorted)
    * removes small objects (_e.g._ small islands have disappeared)
    * smoothes the contours (_e.g._ the coasts are no more jagged)

* - ```{image} greece-closing.png
    ```
  - **Closing** $\bullet$
    * conserve the size of the objects (while they can be slightly distorted)
    * fills small holes (_e.g._ gulfs and lakes are removed)
    * welds close shapes (_e.g._ some separated islands now form only one)
````