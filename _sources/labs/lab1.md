(lab1)=
# Lab 1

> **Indiquer comment lancer jupyter (Ubuntu > terminal > jupyter lab)**

> **Préciser les versions des modules nécessaires (certains étus ont sur leur PC perso des anciennes versions, valable aussi pour les PC de l'école)**


* Exo supplémentaire : affichage d'une image hyperspectrale.
  L'image hyperspectrale Indian\_pines.mat est de taille $145\times145$ pixels et contient 220 bandes spectrales.
  \item Affichez la dixième bande de l'image.
  \item Créez une composition RVB de l'image et affichez-la.
  Vous pouvez pour cela avoir besoin d'effectuer une moyenne (\syntax{mean})
  et de normaliser les bandes pour forcer leurs intensités à être entre 0 et 1.
  \item Affichez les spectres de quelques pixels, par exemple les pixels (34,106), (47,20) et (91,136).
  Utilisez la fonction \syntax{squeeze} qui permet d'éliminer les dimensions vide d'une matrice 3D.
  L'image hyperspectrale Indian\_pines.mat a été capturée en 1992 par le capteur Aviris
  au dessus de champs dans l'Indiana, États-Unis.
  C'est une image de $145\times145$ pixels et 220 bandes spectrales réparties entre 400 et 2500 nm.
  
  
## Operations

* Exo supplémentaire : addition de plusieurs images pour constater que le bruit diminue


## Histogram

* Rajouter un exercice où je demande aux étus de représenter l'histogram d'une image simple 4x4.

* Exo supplémentaire : influence du nb de bins

===


## 07/10/2020 (TP 1)

Indiquer de booter sous Ubuntu. Indiquer comment lancer jupyter (terminal > jupyter lab).

Gérer le test Moodle en début de séance avec 4 salles infos et les retardataires, c'était sport ! Mais ça s'est passé... Avec l'habitude ça devrait mieux se passer.

En TP, les étudiants ont à peu près tous terminés "Setting the intensity range". Pas de difficulté particulière, ni en Python ni en TI.

Toutefois, il faut prévoir une meilleure intro à Python, Jupyter, le concept de notebook, les cellules. Par exemple en développant le premier exo.

La syntaxe "f[m1:m2, n1:n2, b] = x" n'est pas clair pour certains étudiants : ils ne comprennent pas que ça permet d'accéder à des pixels, ni comment s'en servir.

Problèmes :
- contrôle : Delquignies + Brisville
- retards : de Mathelin + Bannery (médecins tous les deux => AJ)
- quelques étudiants sur Zoom mais je n'ai pas communiqué avec eux (coupure wifi de mon côté, et aucun retour de leur part) : PAILLER, ULLMANN?, GIBERT, CLARET
- C. NIOLA et P. AUDIN m'avait indiqué être à distance, mais ne se sont pas connecté à Zoom.


## 14/10/2020 (TP 2)

Le contrôle peut durer moins de 10 min, car beaucoup ont fini à 5 min.

Harmoniser l'utilisation de numpy.fft plutôt que scipy.fft ?

Problèmes :
- contrôle : LODS (cf copie d'écran)


## 21/10/2020 (TP 3)


## 04/11/2020 (TP 4, EAD)

J'ai partagé en 44 salles (par binôme), et les 4 intervenants se sont répartis ces salles. Ainsi, on peut aller voir tout le monde (mais c'est rare quand on va voir un binôme 2 fois, par manque de temps).

Difficultés : calcul du Dice (comment faire l'intersection ? types des images différents, ==, etc.) => faire un point à un certain moment pour éviter que ce calcul prenne trop de temps.

Les étus sont arrivés au seuillage adaptatif (donc les premières questions leur prenne du temps !

## 18/11/2020 (TP 5, EAD)

Les étus n'ont abordé que le débruitage, en général ils implémentent la courbe de l'EQM en fonction du paramètre de la méthode de débruitage. Donc a priori, rien à modifier dans le sujet.

La partie déconvolution ne sert donc qu'aux meilleurs étudiants qui vont loin.

À travers le contrôle, je me rends compte qu'un très grand nombre d'étudiants considère que pour régler lambda, il faut minimiser le critère (alors que la minimisation du critère permet d'avoir l'image, et non lambda) : "lambda (paramètre de régularisation) est trouvé en résolvant un problème d'optimisation". Pour certains, le principe de l'optimisation n'est pas clair : il disent que lambda est réglé à la main avec une procédure d'optimisation. "Lambda est le paramètre de régularisation. Il est choisit par l'utilisateur. C'est un problème d'optimisation. "


## 25/11/2020 (TP 6, EAD)

Les plus rapides sont arrivés jusqu'au tracé des lignes de Hough sur l'image, mais on fait le TP de façon superficielle, en observant l'influence des paramètres sans chercher à comprendre si c'était en accord avec la théorie ou chercher à l'expliquer. Ceux qui ont pris le temps de faire un travail en profondeur, ou les plus lents, abordaient Harris. Donc le TP est plutôt bien calibré, mais il reste à ajouter une "contrainte" pour que les étus se posent des questions.

Introduire dans le book la prononciation de Houg
