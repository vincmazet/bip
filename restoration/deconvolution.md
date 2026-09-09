(C:deconvolution)=
# Deconvolution

Usually, images acquired by a vision system suffer from degradation that can be modelled as a convolution.
For example, some images present a camera shake effect ({numref}`F:deconvolution:example-motion`)
or a blur due to poor focus ({numref}`F:deconvolution:example-blur`).
The goal of deconvolution is to cancel the effect of a convolution.

```{figure} budapest.jpg
---
width: 400px
name: F:deconvolution:example-motion
---
An example of motion blur (the parliament of Budapest shot by a camera).
```

```{figure} ganymede.png
---
width: 300px
name: F:deconvolution:example-blur
---
Hubble's view of Ganymede in 1996.
```

<!-- rosetta.jpg / Example of poor focus blur (Rosetta spacecraft last image). -->

The degradation phenomenon is modelled as in {numref}`F:deconvolution:model`:
The observed image $y$ is degraded by the convolution with a PSF $h$ and, possibly, by a noise $b$ (considered to be additive).

$$
y = h*x + b
$$

The deconvolution computes a deconvolved image $\widehat{x}$ from the observation $y$.
We will consider only linear methods, thus deconvolution comes to filtering by $g$:

$$
\widehat{x} = g*y
$$

```{figure} model-deconvolution.png
---
width: 500px
name: F:deconvolution:model
---
Deconvolution model.
```

Deconvolution needs a degradation model, thus having knowledge about both $h$ and $b$.

* The PSF $h$ can be estimated by observation, _i.e._ by finding in the image some factors to estimate $h$.
  For example, a single point object in the image is $h$.
  The PSF can also be estimated by experimentation by reproducing the observation conditions in a laboratory.
  So, the image of a pulse gives an estimate of $h$.
  Finally, it is also possible to estimate the PSF from a mathematical model of the physics of the observation.
  Note also that some deconvolution methods estimate the PSF $h$ at the same time as $x$:
  these are called blind deconvolution methods (French: _déconvolution myope_).
  
  <!-- développer le 1er exemple, notamment avec une illustration en astro -->
  <!-- 1er point : déconvolution naïve en l'absence de bruit dans une petite zone, essai--erreur, ..-->

* Models for the noise have already been presented in chapter {ref}`C:denoising`.


## Inverse filter

The inverse filter is the simplest deconvolution method.
Since the degradation is modelled $y = h*x + b$, then this equation becomes in the Fourier domain:

$$
Y = HX + B
$$

so we can write:

$$
X = \frac{Y-B}{H}.
$$

We obtain $x$ by calculating the inverse Fourier transform of the previous expression:

$$
x = \mathcal{F}^{-1} \left[ \frac{Y-B}{H} \right].
$$

As the noise (and therefore its spectrum $B$) is unknown,
we can approximate the expression of $x$ by cancelling $B$ in the previous expression,
and thus get the deconvolved image:

$$
\widehat{x} = \mathcal{F}^{-1} \left[ \frac{Y}{H} \right]
$$

The result of the inverse filter applied on an image is given {numref}`F:deconvolution:inverse-filter`.
The result is not usable, and yet the observed image is very little blurred with very little noise!

```{figure} inverse-filter.svg
---
name: F:deconvolution:inverse-filter
---
Result of the inverse filter.
```

The catastrophic result of the inverse filter is due to the fact of having considered the noise to be zero.
Indeed, according to the definition of $\widehat{x}$ and considering $Y = HX + B$, then:

$$
\widehat{x}
= \mathcal{F}^{-1} \left[ \frac{Y}{H} \right]
= \mathcal{F}^{-1} \left[ X + \frac{B}{H} \right]
= x + \mathcal{F}^{-1} \left[ \frac{B}{H} \right]
$$

Thus, the deconvolved image $\widehat{x}$ corresponds to $x$ with an additional term which is the inverse Fourier transform of $B/H$.
The PSF $H$ is generally a low-pass filter, so the values of $H(m,n)$ tend towards $0$ for high frequencies $(m,n)$.
Because $H$ is in the denominator, this tends to drastically amplify the high frequencies of the noise,
and then the term $B/H$ quickly dominates $X$.
This explains the result of {numref}`F:deconvolution:inverse-filter`.

One solution consists in considering only the low frequencies of $Y/H$.
This is equivalent to truncating the result given by the inverse filter by cancelling the high frequencies before calculating the inverse Fourier transform.
The result of the deconvolution is much more acceptable, as shown by {numref}`F:deconvolution:truncated-inverse-filter`,
although the result is still far from perfect (there are many variations in intensity around objects, such as tree trunks)...

```{figure} truncated-inverse-filter.svg
---
name: F:deconvolution:truncated-inverse-filter
---
Result of the truncated inverse filter with very small noise.
```


## Wiener Filter

Wiener filter, denoted by $g$ (with Fourier transform $G$), applies to the observation $y$ such that:

$$
\widehat{x} = g * y
\qquad\Leftrightarrow\qquad
\widehat{X} = GY.
$$

This filter is established in the statistical framework: the image $x$ and the noise $b$ are considered to be random variables.
They are also assumed to be statistically independent.
As a result, the observation $y$ and the estimate $\widehat{x}$ are also random variables.

The calculations are done in the Fourier domain for simplicity (since convolutions become multiplications).
The goal of Wiener filter is to find the image $\widehat{X} = \mathcal{F}[\widehat{x}]$ closest to $X = \mathcal{F}[x]$,
in the sense of the mean squared error $\mathrm{MSE} = \mathbb{E}\left[(\widehat{X}-X)^2\right]$.
Thereby :

$$
\mathrm{MSE}
&= \mathbb{E}\left[(\widehat{X}-X)^2\right] \\
&= \mathbb{E}\left[(GY-X)^2\right] \\
&= \mathbb{E}\left[\big(G(HX+B)-X\big)^2\right] \\
&= \mathbb{E}\left[\big((GH-I)X+GB\big)^2\right]
$$

where $I$ is an image filled with 1.
So:

$$
\mathrm{MSE} = \mathbb{E}\Big[ (GH-I)^*(GH-I)X^*X + (GH-I)^*GX^*B + G^*(GH-I)B^*X + G^*GB^*B \Big]
$$

where $\cdot^*$ denotes the conjugate of the variables.
Since the expectation $\mathbb{E}$ is linear and only $X$ and $B$ are random variables,
we can decompose the previous expression into four terms:

$$
\mathrm{MSE}
= &   (GH-I)^*(GH-I) \,\mathbb{E}\big[X^*X\big]\\
  & + (GH-I)^*G      \,\mathbb{E}\big[X^*B\big]\\
  & + G^*(GH-I)      \,\mathbb{E}\big[B^*X\big]\\
  & + G^*G           \,\mathbb{E}\big[B^*B\big].
$$

Since $X$ and $B$ are independent, then the covariances $\mathbb{E}\big[X^*B\big]$ and $\mathbb{E}\big[B^*X\big] $ are zeros.
Moreover, $\mathbb{E}\big[X^*X\big]$ and $\mathbb{E}\big[B^*B\big]$ are the power spectral densities denoted as $S_x$ and $S_b$
(the power spectral density is the expectation of the square of the modulus of the Fourier transform).
So the mean squared error simplifies into:

$$
\mathrm{MSE} = (GH-1)^*(GH-1) S_x + G^*G S_b
$$

We look for the filter $G$ that minimizes the MSE, or equivalently, that cancels the derivative of MSE:

$$
                       & \frac{\partial \mathrm{MSE}}{\partial G} = (GH-1)^*H S_x + G^* S_b = 0 \\
  \Leftrightarrow\quad &G^*H^*H S_x - H S_x + G^* S_b = 0  \\
  \Leftrightarrow\quad &G^* ( H^*H S_x + S_b) = H S_x  \\
  \Leftrightarrow\quad &G^* = \frac{H S_x}{H^*H S_x + S_b}  \\
  \Leftrightarrow\quad &G = \frac{H^* S_x}{H^*H S_x + S_b}  \\
  \Leftrightarrow\quad &G = \frac{H^* S_x}{|H|^2 S_x + S_b}
$$

Here we are, we get the expression of the Wiener filter $G$! 🥳
Finally, the deconvolved image is the inverse Fourier transform of $GY$:

$$
\widehat{x} = \mathcal{F}^{-1} \Bigg[\frac{H^* S_x}{|H|^2 S_x + S_b} Y \Bigg]
$$

We can consider that the power spectral densities $S_x$ and $S_b$ are constant
(for $S_b$, it is necessary to assume white noise).
Thus, the expression of the Wiener filter can be written

$$
\widehat{x} = \mathcal{F}^{-1} \Bigg[ \frac{H^*}{|H|^2 + S_b/S_x} Y \Bigg]
$$

and the term $S_b/S_x$ is replaced by a constant $K$, which becomes the parameter of the method, to be set by the user.

Two remarks:

* where $H$ vanishes (typically in high frequencies),
  the problem of noise increase is no longer observed as with the inverse filter,
  since the inverse filter tends towards 0,

* moreover, if the noise in the image is zero, then $S_b = 0$ and Wiener filter comes back to the inverse filter:

  $$
  \widehat{x}
  = \mathcal{F}^{-1} \Bigg[ \frac{H^*}{|H|^2} Y \Bigg]
  = \mathcal{F}^{-1} \Bigg[ \frac{Y}{H} \Bigg]
  $$
  
The result of Wiener filter is presented {numref}`F:deconvolution:wiener-filter`:
it is clearly much better than the inverse filter, even its truncated version!

```{figure} wiener-filter.svg
---
name: F:deconvolution:wiener-filter
---
Result of Wiener filter
($\lambda$ is set so that the estimation is the best in terms of MSE).
```


<!-- Cela dit, il n'est pas juste de comparer ces deux méthodes sur la {numref}`F:deconvolution:wiener`,
car les paramètres des méthodes (10% et $K=10^{-5}$) ne sont peut être pas les meilleurs.
Il se pose donc la question : comment régler le paramètre de chaque méthode ?

```{margin}
L'EQM dont il est question ici n'est pas au sens statistique, comme ci-avant.
Il s'agit ici du carré de la différence entre les deux images.
```

Pour y répondre, la {numref}`F:deconvolution:parametre` représente la qualité du résultat, en termes d'EQM,
en fonction de ces paramètres.
On constate que pour le meilleur choix des paramètres (point rouge sur la courbe),
l'EQM est bien meilleure pour le filtre de Wiener que pour le filtre inverse.
Le résultat correspondant est représenté {numref}`F:deconvolution:wiener-best`.
La différence sur cette sous-image est assez faible, mais il n'empêche que le dessin sur la voile est plus net avec le filtre de Wiener.

```{figure} figs/restauration15.png
---
width: 600px
name: F:deconvolution:parametre
---
Comparaison de l'EQM en fonction du paramètre de la méthode, pour le filtre inverse tronqué et le filtre de Wiener.
```

```{figure} figs/restauration16.png
---
width: 600px
name: F:deconvolution:wiener-best
---
Résultat du filtre inverse tronquée et du filtre de Wiener pour les meilleurs choix de paramètres.
``` -->
