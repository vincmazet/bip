(P:registration:deformation)=
# Deformation model

:::{caution}
This page is currently being written and will be ready in a few days.
:::



**////-> éléments sur la pyramide (dans la partie interpolation je crois) (formation des images)**

Geometric transformation ? rescale/resize, rotation, translation, stretch, shearing... (cf Jahne fig 10.16 p. 277 + fig 10.15 p. 276) 



## Transform model

La déformation appliquée à l'image source est une transformation mathématique qui peut être linéaire ou non.

Une transformation linéaire s'écrit :

$$
  p' = M p
$$

où
* $p = [x \; y \; 1]^T$ regroupe les coordonnées du pixel $(x,y)$ de l'image source,
* $p' = [x' \; y' \; 1]^T$ regroupe les coordonnées du pixel $(x',y')$ de l'image déformée,
* $M \in \mathbb{R}^{3\times3}$ est la matrice de transformation.

Par exemple, si la matrice de déformation est

$$
  M = \begin{bmatrix}
    1 & 0 & t_x \\
    0 & 1 & t_y \\
    0 & 0 & 1
  \end{bmatrix}
$$

alors

$$
  p' = \begin{bmatrix}
    x' \\
    y' \\
    1
  \end{bmatrix}
  = \begin{bmatrix}
    x + t_x \\
    y + t_y \\
    1
  \end{bmatrix}
$$

Les coordonnées du pixel $p'$ de l'image transformée
correspondent à celle du pixel $p$ de l'image source
après une translation de de $t_x$ pixels en $x$ et $t_y$ pixels en $y$.

```{note}
Notez que la définition de $p'$ à partir de $p$ peut résulter en une image transformée composée de pixels vides
si aucun pixel $p$ de l'image originale $f$ ne tombe sur un pixel $p'$ de l'image transformée $f'$.
Pour éviter cela et obtenir la valeur de tous les pixels $p'$,
on applique l'inverse de la transformation pour trouver la coordonnée (souvent non entière) dans l'image originale $f$.
Une interpolation permet de déterminer la valeur de cette coordonnée, et donc du pixel $p'$.
```

Les différents types de déformations sont illustrés ci-après
sur l'image représentée {numref}`F:registration:lena-defnull`.

```{figure} XXX/lena-defnull.png
---
scale: 50%
name: F:registration:lena-defnull
---
Image Lena.
```

### Déformation rigide

Une déformation rigide (ou euclidienne) est une transformation linéaire
définie avec 3 paramètres : $\theta=\{\alpha,t_x,t_y\}$.
La déformation rigide regroupe donc une rotation d'angle $\alpha$ et une translation $(t_x,t_y)$.
La matrice de déformation s'écrit :

$$
  M\!=\!\begin{pmatrix}
    \cos\alpha & \sin\alpha & t_x \\
    -\sin\alpha & \cos\alpha & t_y \\
    0 & 0 & 1
  \end{pmatrix}
$$

```{figure} XXX/lena-defrigide.png
---
scale: 50%
name: F:registration:lena-defrigide
---
Exemple de déformation rigide.
```

### Déformation affine

Une déformation affine est une transformation bilinéaire définie
avec 6 paramètres : $\theta=\{m_{11}, m_{12}, m_{13}, m_{21}, m_{22}, m_{23}\}$.
L'image subit une mise à l'échelle et un cisaillement : les droites parallèles restent parallèles après déformation, mais les angles changent.
La matrice de déformation s'écrit :

$$
  M\!=\!\begin{pmatrix}
    m_{11} & m_{12} & m_{13} \\
    m_{21} & m_{22} & m_{23} \\
    0 & 0 & 1
  \end{pmatrix}
$$


```{figure} XXX/lena-defaffine.png
---
scale: 50%
name: F:registration:lena-defaffine
---
Exemple de déformation affine.
```

### Déformation perspective

Une déformation perspective est une transformation linéaire définie
avec 9 paramètres : $\theta=\{m_{11}, m_{12}, m_{13}, m_{21}, m_{22}, m_{23}, m_{31}, m_{32}, m_{33}\}$.
La matrice de déformation s'écrit :

$$
  M\!=\!\begin{pmatrix}
    m_{11} & m_{12} & m_{13} \\
    m_{21} & m_{22} & m_{23} \\
    m_{31} & m_{32} & m_{33}
  \end{pmatrix}
$$

```{figure} XXX/lena-persp.png
---
scale: 50%
name: F:registration:lena-persp
---
Déformation perspective.
```

### Déformation non linéaire

On peut définir tout autre type de déformation sans passer par une transformation linéaire.
Ainsi, l'utilisation de fonctions 2D spécifiques (polynôme, sinusoïde, spline, ondelette...)
ou d'un champ de déformation non paramétrique est envisageable.

Il peut alors être nécessaire d'introduire des contraintes sur le modèle de déformation
(préservation de la topologie, douceur, symétrie...).

```{figure} XXX/lena-deffnonlin.png
---
scale: 50%
name: F:registration:lena-deffnonlin
---
Déformation non linéaire.
```
