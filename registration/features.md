(P:registration:features)=
# Feature detection



**////-> éléments sur la pyramide (dans la partie interpolation je crois) (formation des images)**



## Image characteristics

La déformation à appliquer sur l'image source est basée sur des caractéristiques de cette image.
Le choix des caractéristiques utilisées conduit à l'une des deux méthodes de recalage décrite ci-après.

### Approche iconique

L'approche iconique (_intensity-based registration_) <!-- OU _DIRECT (PIXEL-BASED) ..._ ? -->
se base directement sur l'intensité des pixels de l'image.
Ainsi, toute l'information contenue dans l'intensité des pixels est utilisée.
À la place de l'image elle-même, on peut aussi utiliser une de ses transformations (Fourier, ondelette, gradient...).

L'avantage de l'approche iconique est quelle est relativement bien automatisée.

Les inconvénients de l'approche iconique sont
le coût calculatoire important et la mémoire nécessaire,
mais elle est également sensible au bruit et aux variations d'intensité entre les images.

### Approche géométrique

Dans l'approche géométrique (_feature-based registration_),
la déformation à appliquer à l'image source n'est pas définie à partir des intensités des pixels,
mais à partir de caractéristiques particulières de l'image.
Ces primitives peuvent être :
* intrinsèques à l'image : on se base sur les coins, les contours des objets, etc.
* extrinsèques à l'image : on se base sur des marqueurs insérés sur les objets.
Il faut ensuite apparier les primitives (_feature matching_).

```{figure} XXX/vincent18.png
---
height: 200px
name: F:registration:feature-based
---
Appariement de primitives entre deux images.
```

Les avantages de l'approche géométrique sont d'utiliser peu de données de l'image,
impliquant un coût calculatoire faible.

Les inconvénients de l'approche géométrique sont que :
* l'appariement des primitives peut être difficile à effectuer,
* la qualité du recalage dépend de la précision de l'extraction des primitives,
* la précision du recalage n'est garantie qu'au voisinage des primitives.
