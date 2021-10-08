# Region growing



<!-- region vs intensity : l'aspect spatiale (voisinage entre pixels) pris en compte

La limite fondamentale des méthodes précédentes est
de ne pas prendre en compte l'information de voisinage :
seule l'information de distribution des intensités est utilisée.

À l'inverse, les méthodes basées région sont capables d'agréger des pixels spatialement proches _et_ ayant des intensités similaires.
Nous allons voir deux méthodes basées régions :
* la croissance de région
* la méthode de décomposition/fusion


## Croissance de région

Le principe de la croissance de région (_region growing_) est, à partir d'un pixel initial (appelé « germe »),
d'étendre la région en y ajoutant les pixels du voisinage qui satisfont le critère d'homogénéité,
comme l'illustre la {numref}`F:segmentation:regiongrowing`.

```{figure} figs/segmentation-regiongrowing.png
---
height: 250px
name: F:segmentation:regiongrowing
---
Illustration de la croissance de région (le germe est indiqué par la croix rouge).
```

Le choix du germe peut se faire manuellement ou automatiquement
(par exemple en choisissant au hasard un pixel en dehors des zones de fort contraste).

Le critère de similarité est le suivant :
si un pixel $f(m,n)$ et une région $R$ sont suffisamment similaires, alors ils sont fusionnés ; sinon une nouvelle région est créée.
On peut utiliser par exemple le critère 

$$
  \left| f(m,n) - \mu_R \right| < T \sigma_R
$$

Ainsi, si le paramètre $T$ est élevé, il sera facile d'agréger des nouveaux pixels à la région.
Au contraire, si $T$ faible alors il sera plus difficile d'agréger des nouveaux pixels à la région. -->

<!-- Choix de la connexité : 4-voisinage ou 8-voisinage. -->

<!-- * $R$ : région segmentée, initialisée au germe
* $S$ : pixels à tester, initialisé au voisinage du germe (file FIFO : \emph{first in, first out})
Algorithme :
  \setlength{\fboxsep}{3mm}
  \colorbox{algobg}{\parbox{.9\textwidth}{
  tant que $S$ n'est pas vide :
  \albar $p$ est le premier pixel de la liste $S$
  \albar $p$ est retiré de $S$
  \albar si $p$ est homogène avec $R$ :
  \albar\albar ajout à $R$ de $p$
  \albar\albar ajout à $S$ des pixels du voisinage de $p$ qui ne sont pas dans
  \albar\albar\qquad $R$ et qui ne sont pas incompatibles.
  \albar sinon :
  \albar\albar $p$ est marqué comme incompatible.
 -->

<!-- La croissance de région ne fournit pas directement une partition de l'image,
mais permet de segmenter une ou plusieurs structures d'intérêt via la sélection de germes adaptés.
Pour segmenter une image en $K$ classes, il faudra donc $K$ germes. -->

<!-- Au moins deux points germes sont nécessaires :
  \imgbox{45mm}{eclairs}{Image originale}\qquad
  \imgbox{45mm}{eclair1}{Image segmentée} -->

<!-- Quelle segmentation est obtenue avec la plus grande valeur de $T$ ?
    \imgbox{40mm}{eclair1}{\only<1>{A}\only<2>{$T$ petit}\phantom{gT}}\qquad
    \imgbox{40mm}{eclair3}{\only<1>{B}\only<2>{$T$ grand}\phantom{gT}}% -->

<!-- % TODO : ??? \textcolor{red!70}{Rq : en cas d'utilisation de statistique globale pour le test d'homogénéité, l'ordre de traitement des pixels peut influencer le résultat final.} -->


<!-- ## Décomposition/fusion

La méthode de décomposition/fusion (_split and merge_) fonctionne en deux étapes :
1. d'abord, l'image est décomposée successivement en régions
   si elles ne satisfont pas le critère d'homogénéité.
   Cela permet d'aboutir à une première partition de l'image ;
1. ensuite, les régions obtenues sont fusionnées si elles sont adjacentes et qu'elles vérifient le critère d'homogénéité. -->

<!-- \onslide<4->{Les représentations en arbre et par graphe permettent une représentation haut niveau de l'image.} -->


<!-- **Décomposition**

La décomposition est une procédure itérative.
Au départ, il n'y a qu'une seule région qui correspond à l'image toute entière.
À chaque itération, les régions qui ne vérifient pas le critère d'homogénéité sont divisées en quatre nouvelles régions de taille identique.
La procédure s'arrête lorsque les régions sont toutes homogènes ;
au pire, les régions les plus petites sont ainsi des pixels uniques.

On peut utiliser une représentation en quad-arbre (_quad-tree_) de cette décomposition :
c'est une arborescence dont chaque nœud représente une région et possède quatre fils,
la racine représente l'image entière. -->

<!-- 
```{figure} figs/segmentation-split-merge-quadtree.gif
---
height: 300px
name: F:segmentation:split-merge-quadtree
---
Illustration de la décomposition avec représentation en quad-arbre.
```
 -->
 
<!-- Finalement, la méthode de décomposition par quad-arbre fait apparaître des régions carrées sur l'image segmentée.
Le problème majeur de cette décomposition provient de la rigidité des divisions réalisées sur l'image,
mais au moins cela fournit une partition initiale de l'image.

**Fusion**

La partition de l'image obtenue avec la la représentation en quad-arbre
peut être vue comme un graphe d'adjacence (RAG : _region adjacency graph_).
C'est une nouvelle représentation, sous forme de graphe, dont :
* les nœuds correspondent à une région de l'image,
* les arêtes relient les nœuds correspondants à deux régions adjacentes (ayant une frontière commune).
La {numref}`F:segmentation:rag` donne un exemple de tel graphe.

```{figure} figs/vincent88.png
---
height: 200px
name: F:segmentation:rag
---
Une image segmentée et sa représentation sous forme de graphe d'adjacence.
```

Donc, à partir de ce graphe d'adjacence, les nœuds $R_1$ et $R_2$ voisins et dont le critère de similarité sur $R_1 \cup R_2$ est respecté
sont fusionnés (cf. {numref}`F:segmentation:split-merge-rag`).

```{figure} figs/segmentation-split-merge-rag.gif
---
height: 300px
name: F:segmentation:split-merge-rag
---
Illustration de la fusion avec représentation en graphe d'adjacence.
```
 -->