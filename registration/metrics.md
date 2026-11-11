(P:registration:metrics)=
# Similarity metrics



**////-> éléments sur la pyramide (dans la partie interpolation je crois) (formation des images)**



## Interpolation and similarity criterion

Connaissant les paramètres de déformation $\theta$ à appliquer sur l'image,
la transformation correspondante peut être effectuée.
Il s'agit d'un problème d'[interpolation](C:interpolation).

Le critère de similarité (_error metric_) $E(\theta)$ représente la distance (au sens mathématique)
entre l'image de référence $g$ et l'image déformée $f'$
(obtenue an appliquant le modèle de déformation de paramètres $\theta$ sur l'image source $f$).
Cette distance est minimale lorsque les deux images se superposent au mieux,
c'est-à-dire lorsque la similarité entre l'image de référence $g$ et l'image déformée $f\,'$ est maximale.

L'objectif du recalage est de trouver les paramètres $\theta$ qui minimisent le critère de similarité $E(\theta)$ :
c'est donc un problème d'optimisation.
Le choix de $E$ dépend quant à lui du choix de l'approche choisie.

### Approche iconique

Dans le cas d'une approche iconique (basée sur l'intensité des pixels),
on utilisera un critère de similarité dit _dense_.
Il existe plusieurs hypothèses sur les liens entre les intensités des deux images.
Dans le cas le plus simple, on suppose que les intensités des pixels
sont égales à un bruit additif gaussien près,
donc le critère de similarité peut être la distance euclidienne,
qui est proportionnelle à l'erreur quadratique moyenne (EQM) :

$$
  E(\theta) = \sum_{m=1}^M \sum_{n=1}^N \big(f\,'(m,n) - g(m,n)\big)^2
$$

### Approche géométrique

Dans le cas d'une approche géométrique (basée sur des caractéristiques),
on utilisera une distance entre ces primitives.

* Par exemple, dans le cas où les primitives sont des pixels particuliers,
  on peut considérer la distance entre ces pixels avec la norme euclidienne :

  $$
    E(\theta) = \sum_{n=1}^N (x_n-x'_n)^2 + (y_n-y'_n)^2
  $$

  où $(x_n,y_n)$ et $(x'_n,y'_n)$ sont les coordonnées des pixels appariés.

* Un autre exemple est le cas où les primitives sont des courbes.
  L'algorithme ICP (_Iterative Closest Point_) peut être utilisé pour déterminer une distance entre ces deux courbes, définie comme

  $$
    E(\theta) = \sum_{n=1}^N d_n^2
  $$

  où $d_n$ est la distance entre chaque point de la courbe 1 avec le point le plus proche de la courbe 2.

  ```{figure} XXX/icp.png
  ---
  height: 150px
  name: F:registration:icp
  ---
  Distance entre deux courbes avec l'algorithme ICP.
  ```

### Optimisation du critère de similarité

Comme on l'a dit précédemment, on cherche les valeurs des paramètres $\theta$
de la transformation qui minimise $E(\theta)$.
Mathématiquement, le problème s'écrit :

$$
  \hat{\theta} = \arg \min_{\theta} E(\theta)
$$


```{figure} XXX/optim.png
---
height: 200px
name: F:registration:optim
---
Principe de l'optimisation d'un critère $E$ :
exemple pour $\theta=\alpha$ dans le cas d'une simple rotation.
```

Il existe énormément de méthodes d'optimisation dont la description dépasse le cadre de ce cours :
* Solution explicite (en annulant la dérivée de $E$),
* Recherche exhaustive (toutes les possibilités sont testées),
* Méthodes déterministes :
  algorithme du simplexe, descente de gradient, gradient conjugué,
  algorithme de Levenberg-Marquardt, etc.
* Méthodes stochastiques :
  recuit simulé, algorithmes génétiques, gradient stochastique, etc.

<!-- solution explicite : méthode procustéenne, (_exact point matching_) -->

On peut combiner ces méthodes d'optimisation avec des schémas hiérarchiques (_hierarchical / coarse to fine approaches_) :
l'idée est de décomposer le problème initial en plusieurs petits problèmes de complexité moindre.
Cela a tendance à réduire le risque de convergence vers un minimum local et à accélérer le calcul.
On peut donc utiliser une approche par multi-résolution
(on commence par effectuer l'optimisation sur une image très sous-échantillonnée
et affiner l'optimisation à des échelles progressivement plus proches de l'image originale).
On peut également, en particulier dans le cas d'un modèle de déformation complexe,
commencer par optimiser un modèle simple (déformation rigide par exemple)
puis le complexifier petit à petit.

Approches hiérarchiques

L'idée des approches hiérarchiques (_hierarchical / coarse to fine approaches_)
est de décomposer le problème initial en plusieurs petits problèmes de complexité moindre.
Cela a tendance à réduire le risque de convergence vers un minimum local et à accélérer le calcul.

* Dans le cas de données complexes, on adoptera une approche par multi-résolution :
  on commence par effectuer l'optimisation sur une image très sous-échantillonnée (niveau 0),
  et refaire l'optimisation à différentes échelles jusqu'à l'image originale.
  Chaque algorithme d'optimisation est initialisé avec la valeurs de $\theta$ obtenue
  au niveau précédent.

  ```{figure} XXX/multiresolution.png
  ---
  height: 200px
  name: F:registration:multiresolution
  ---
  Exemple : pyramide gaussienne.
  ```

* Dans le cas d'un Modèle de déformation complexe,
  on privilégiera une complexification de ce modèle.
  Par exemple, on pourra commencer par considérer une déformation rigide,
  qui sera affinée ensuite en déformation affine voire non rigide.
  On peut aussi utiliser une approche multi-échelle (_multiscale approach_)
  illustrée {numref}`F:registration:multiscale`.

    ```{figure} XXX/multiscale.png
    ---
    height: 100px
    name: F:registration:multiscale
    ---
    Approche multi-échelle.
    ```

% =============================================================================================== %