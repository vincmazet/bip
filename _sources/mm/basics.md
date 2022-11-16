# Basic operators


(mm:dilation)=
## Dilation

Having an image $I$ and a structuring element $E_c$, the dilation (french: _dilatation_)
of $I$ by $E_c$ is noted $I \oplus E_c$.
The result of the dilation is obtained by moving the origin of the structuring element onto the white pixels of the image
and keeping the set of pixels of each displaced structuring element.

Mathematically speaking:

$$
  I \oplus E_c = \{ E_c \mid c \in I \}
$$

```{figure} dilation-toy.svg
---
name: mm:dilation-toy
---
Example of dilation on a small image $I$ by the structuring element $E_c$
(with the origin $c$ is at the centre and represented by the blue dot).
```

The structuring element is often described with a matrix.
So, the structuring element in {numref}`mm:dilation-toy` is written as:

$$
E =
\begin{pmatrix}
0 & 1 & 0 \\
1 & 1 & 1 \\
0 & 1 & 0 \\
\end{pmatrix}.
$$

Note that the matrix does not consider the zero pixels surrounding the main part of $E$.


### Properties

* Dilation is a binary operation and is not linear.
  Therefore, it cannot be expressed as convolution which is a linear mathematical operator.

* Dilation is associative, _i.e._ the application of two consecutive dilations can be done in any order:

  $$
    (I \oplus  E_1 ) \oplus  E_2 = (I \oplus  E_2) \oplus  E_1 = I \oplus  (E_1 \oplus E_2)
  $$
  
  (here, the subscripts 1 and 2 mean two different structuring elements.)

* Dilation is a monotonous operation since the relations of inclusions are conserved:

  $$
    I_1 \subseteq I_2  \quad\Rightarrow\quad  I_1 \oplus E_c \subseteq I_2 \oplus E_c
  $$


(mm:erosion)=
## Erosion

The erosion (french: _érosion_) of $I$ by $E_c$ is noted $I \ominus E_c$.
The result of the erosion is obtained by moving the structuring element into the white pixels of the image
and keeping only the origin of each displaced structuring element.

$$
  I \ominus E_c = \{ c \mid E_c \subseteq I\}
$$

```{figure} erosion-toy.svg
---
name: F:mm:erosion-toy
----
Example of erosion on a small image $I$ by the structuring element $E_c$
(with the origin $c$ is at the centre and represented by the blue dot).
```

### Properties

Erosion has similar properties as dilation.

* Erosion cannot be expressed as convolution.

* Erosion is associative:

  $$
    (I \ominus E_1 ) \ominus E_2 = (I \ominus E_2) \ominus E_1 = I \ominus (E_1 \oplus E_2)
  $$
  
  Note that the result of two successive erosions is equivalent to an erosion
  whose structuring element is the _dilation_ of the two first structuring elements.

* Erosion is a monotonous operation:

  $$
    I_1 \subseteq I_2  \quad\Rightarrow\quad  I_1 \ominus E \subseteq I_2 \ominus E
  $$


## Duality

Dilation and erosion are dual operators.
Considering the background as the object and the object as background (_i.e._ by working with the complement of the image),
the dilation is converted to erosion and vice versa:

$$
  I^\mathrm{c} \ominus E = (I \oplus E)^\mathrm{c} \\
  I^\mathrm{c} \oplus E = (I \ominus E)^\mathrm{c}
$$