# Watershed

To do...

<!-- La ligne de partage des eaux (_watershed_) considère l'image comme un carte topographique où :
* les régions de la segmentation sont les vallées
* les frontières entre régions sont les crêtes

Ainsi la {numref}`F:segmentation:watershed-moon` montre, pour une image de la Lune, ce que devrait être la carte topographique correspondante.
Cette carte est en fait la vue 3D de la norme du gradient de l'image.

```{figure} figs/segmentation-watershed-moon.png
---
height: 200px
name: F:segmentation:watershed-moon
---
Une image et son gradient (vu comme une image et comme un signal 3D, faisant apparaître le relief).
```

Le principe de la ligne de partage des eaux est donc :
1. de construire la carte d'élévation,
1. de remplir progressivement d'eau chaque bassin versant : l'eau apparaît tout en bas du relief,
1. de faire monter le niveau de l'eau,
1. lorsque deux bassins se rejoignent, la ligne de partage des eaux est marquée comme frontière.

La {numref}`F:segmentation:watershed-algo` schématise cet algorithme sur une coupe de l'image.

```{figure} figs/segmentation-watershed-algo.gif
---
height: 200px
name: F:segmentation:watershed-algo
---
Schématisation de l'algorithme de ligne de partage des eaux.
``` -->

<!-- Algorithme :
 \setlength{\fboxsep}{3mm}
 \colorbox{algobg}{\parbox{.9\textwidth}{
  Calculer le gradient (ou le Laplacien) de l'image.
  Les pixels ayant l'intensité la plus faible forment les bassins \phantom{\albar}\quad versants initiaux.
  Pour chaque niveau d'intensité $i$ :
  \albar Pour chaque groupe de pixels d'intensité $i$ :\\
  \albar\albar Si adjacent à exactement une région existante :\\\albar\albar\quad ajouter ces pixels dans cette région.\\
  \albar\albar Si adjacent à plusieurs régions simultanément :\\\albar\albar\quad marquer comme ligne de partage des eaux.
  \albar\albar Sinon, commencer une nouvelle région. -->

<!-- Une des limites de cette méthode apparaît lorsqu'il y a beaucoup de minima locaux dans le gradient.
Dit autrement, il y a trop de bassins versants très petits, qui sont alors autant de régions dans la segmentation.
Pour limiter ce nombre, on peut :
* lisser (avec un filtre passe-bas) le gradient avant d'appliquer l'algorithme,
* choisir manuellement les bassins versants d'intérêt avec des marqueurs,
* ou fusionner les minima locaux. -->

% =============================================================================================== %

<!-- ## Snakes

Contours actifs

Principe : à partir d'un contour initial proche de l'objet à segmenter,
le contour évolue de manière itérative et cherche à converger
vers les zones de fort gradient (= contour) sous certaines contraintes (forme, longueur, etc.).

Le contour est modélisé par un ensemble de points (x_i,y_i)
qui se déplacent légèrement à chaque itération pour déformer le contour.

  \includegraphics[width=7cm]{vincent117-1}

Le contour cherche à minimiser une énergie (ou fonction coût)
qui mesure la qualité de la segmentation :

  E_\text{totale} = E_\text{interne} + \lambda E_\text{externe}

* Énergie interne : encourage certaines configurations de forme
  (régularité, élasticité, a priori de forme, ...)
* Énergie externe : encourage le modèle à converger vers les contours des objets
  (zones de fort gradient)

% Différents types d'énergie interne :
%   \includegraphics[width=8cm]{vincent115} -->
