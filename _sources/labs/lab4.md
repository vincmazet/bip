(lab4)=
# Lab 4

<!-- > Difficultés : calcul du Dice (comment faire l'intersection ? types des images différents, ==, etc.) => faire un point à un certain moment pour éviter que ce calcul prenne trop de temps.

> Les étus sont arrivés au seuillage adaptatif (donc les premières questions leur prenne du temps !

> conserver un TP ouvert avec un objectif (segmenter des pièces, on pourrait tout à la fin utiliser regionprops pour les distinguer et trouver leur valeur fiduciaire)


On souhaite segmenter les pièces de monnaie de l'image [coins1.png](https://vincmazet.github.io/ftip/_static/data/coins1.png) en seuillant l'image.

Dans un premier temps, le seuil est choisi visuellement à partir de l'histogramme de l'image.

* Affichez l'histogramme de l'image [coins1.png](https://vincmazet.github.io/ftip/_static/data/coins1.png), et déduisez-en un seuil pour segmenter l'image.
  L'image seuillée `image2` est obtenue à partir de l'image `image1` et le seuil `s` avec la syntaxe
  
  ```
  image2 = image1>s
  ```
  
* Calculez le coefficient Dice de la segmentation obtenue
  en comparant cette dernière à la vérité terrain [coins-groundtruth.png](https://vincmazet.github.io/ftip/_static/data/coins-groundtruth.png).

Dans un deuxième temps, le seuil est déterminé grâce à la méthode de Otsu.

* Utilisez `skimage.filters.threshold_otsu` pour déterminer une valeur de seuil,
  et affichez la segmentation résultante.

* Qu'observez-vous comme différences entre le résultat de cette segmentation
  avec le résultat de la segmentation manuelle ?
  Comment ces différences peuvent-elles s'expliquer ?

Considérons maintenant l'image [coins2.png](https://vincmazet.github.io/ftip/_static/data/coins2.png).

* En quoi cette nouvelle image diffère de la précédente ?

* Segmentez l'image avec le seuil déterminé par la méthode de Otsu sur cette nouvelle image.
  Qu'observez-vous, et comment cela peut s'expliquer ?

Enfin, un seuil adaptatif est appliqué à l'image [coins2.png](https://vincmazet.github.io/ftip/_static/data/coins2.png).
Cela consiste à considérer des portions de l'image et à appliquer un seuillage de Otsu sur chacune d'elles.

* Appliquez un seuillage adaptatif pour segmenter l'image.

* Critiquez la méthode implémentée : identifiez les bons résultats de la méthode et ses limites.
  Proposez des améliorations. -->

<!-- Questions supplémentaires possibles :
- utiliser la ligne de partage des eaux pour distinguer des pièces qui seraient collées
- region growing ?
- contour actifs -->