(P:binary:conclusion)=
# Conclusion

Mathematical morphology is a collection of operators that deal with the shapes of objects.
This chapter focused on some operators that apply to binary images, but there are extensions of these techniques to grayscale images.

Binary images are seen as sets forming objects (represented in white) on a background (represented in black).
We have introduced the notion of connectivity and pixel neighborhood.
The four basic operators of mathematical morphology perform operations by using a (often small) binary image called structuring element.

::::{list-table}
:header-rows: 0
:widths: 10 30

* - :::{image} figs/greece.png
    :::
  - **Original image**

* - :::{image} figs/greece-dilation.png
    :::
  - **Dilation** $\oplus$
    * increases the size of objects (*e.g.* the islands are bigger)
    * fills the small holes (*e.g.* the Gulf of Corinth
      no longer exist after dilation)
    * welds close objects (*e.g.* some islands are grouped into a larger island)

* - :::{image} figs/greece-erosion.png
    :::
  - **Erosion** $\ominus$
    * decreases the size of objects (*e.g.* Crete is smaller)
    * widens the holes (*e.g.* the Gulf of Corinth is bigger)
    * separates the connected objects by a small bridge
      (*e.g.* the Peloponnese and mainland Greece are now disconnected)
    * removes small items (*e.g.* small islands have disappeared)

* - :::{image} figs/greece-opening.png
    :::
  - **Opening** $\circ$
    * conserve the size of the objects (while they can be slightly distorted)
    * removes small objects (*e.g.* small islands have disappeared)
    * smoothes the contours (*e.g.* the coasts are no more jagged)

* - :::{image} figs/greece-closing.png
    :::
  - **Closing** $\bullet$
    * conserve the size of the objects (while they can be slightly distorted)
    * fills small holes (*e.g.* gulfs and lakes are removed)
    * welds close shapes (*e.g.* some separated islands now form only one)
::::

By combining the basic operators, powerful tools can be defined.


:::{seealso} References

* (B:binary:Bloch2005)=
  I. Bloch *et al.*,
  *Le traitement des images*
  ([volume 1](https://perso.telecom-paristech.fr/bloch/ANIM/poly-anim-t1.pdf),
  [volume 2](https://perso.telecom-paristech.fr/bloch/ANIM/poly-anim-t2.pdf)),
  Polycopié du cours ANIM, Télécom-Paris, 2005.

:::