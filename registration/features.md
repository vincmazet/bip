(P:registration:features)=
# Feature detection


Image registration requires reference points in the images to determine the transformation to be applied.
Two families of fetures can be used.
Both families have their respective advantages and limitations, and they can sometimes be advantageously combined.


## Intensity-based (iconic) registration

L'approche iconique (_intensity-based registration_)
se base directement sur l'intensité des pixels de l'image.
Ainsi, toute l'information contenue dans l'intensité des pixels est utilisée.
À la place de l'image elle-même, on peut aussi utiliser une de ses transformations (Fourier, ondelette, gradient...).

L'avantage de l'approche iconique est quelle est relativement bien automatisée.

Les inconvénients de l'approche iconique sont
le coût calculatoire important et la mémoire nécessaire,
mais elle est également sensible au bruit et aux variations d'intensité entre les images.

****

Use all the information contained in the intensities of the image

Several kind of image reprensentation can be considered (Fourier transform, wavelet, differential operators, …)

Pros
fully automatic

Cons
memory and CPU demanding
sensitive to noise and intensity variation between images




### Geometric methods

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



Pros
Sparse representation of the image => low computational burden

Cons
Registration accuracy depends on the accuracy of feature extraction
Accurate matching is guaranteed only in the neighborhood of the features
the matching step can be hard to resolve (not always a one-to-onematching)