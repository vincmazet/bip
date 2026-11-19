(P:restoration:deconvolution)=
# Deconvolution

Images acquired by a vision system suffer from degradation that can generally be modelled as a convolution.
For example, some images present a camera shake effect (@F:restoration:example-motion)
or a blur due to poor focus (@F:restoration:example-blur).
The goal of deconvolution is to cancel the effect of a convolution.

:::{figure} figs/budapest.jpg
:width: 400px
:name: F:restoration:example-motion
An example of motion blur (the parliament of Budapest shot by a camera).
:::

:::{figure} figs/ganymede.png
:width: 300px
:name: F:restoration:example-blur
Hubble's view of Ganymede in 1996.
:::

The degradation phenomenon is modelled as in @F:restoration:deconvolution-model.
The observed image $y$ is obtained from the "clean" image $x$ degraded through convolution with a PSF $h$ and, possibly, by a noise $b$ (considered to be additive):

$$
y = h*x + b
$$

Deconvolution aims to estimate a restored image $\widehat{x}$ from the observation $y$.
We will consider only linear methods, thus deconvolution is implemented by filtering $y$ by $g$:

$$
\widehat{x} = g*y
$$

:::{figure} figs/deconvolution-model.png
:width: 500px
:name: F:restoration:deconvolution-model
Deconvolution model.
:::

A knowledge about the degradation model (i.e. $h$ and $b$) is necessary to perform deconvolution.

* The PSF $h$ can be estimated empirically from the observed image $y$ itself.
  For instance, a single point object directly yields $h$.
  Alternatively, the PSF can be estimated experimentally by reproducing the observation conditions in a laboratory:
  the image of a point source gives an estimate of $h$.
  It is also possible to estimate the PSF from a mathematical model of the imagging system.
  Note finally that certain deconvolution methods estimate the PSF $h$ at the same time as $x$:
  these are refered to as blind deconvolution methods (French: _déconvolution myope_).

  <!-- développer le 1er exemple, notamment avec une illustration en astro -->
  <!-- 1er point : déconvolution naïve en l'absence de bruit dans une petite zone, essai--erreur, ..-->

* Models for the noise have already been presented in @P:restoration:denoising.

<!------------------------------------------------------------------------------------------------>

## Inverse filter

The inverse filter is the simplest deconvolution method.

The degradation model $y = h*x + b$ becomes in the Fourier domain:

$$
Y = HX + B
\quad\Leftrightarrow\quad
X = \frac{Y-B}{H}.
$$

We obtain $x$ by calculating the inverse Fourier transform of the previous expression:

$$
x = \mathcal{F}^{-1} \left[ \frac{Y-B}{H} \right].
$$

As the noise (and therefore its spectrum $B$) is unknown,
we can approximate the expression of $x$ by cancelling $B$ in the previous expression.
Consequently, the deconvolved image is defined as:

$$
\widehat{x} = \mathcal{F}^{-1} \left[ \frac{Y}{H} \right]
$$

The result of the inverse filter applied on an image is given @F:restoration:inverse-filter.
The result is not usableand yet the observed image is very little blurred with very little noise!

:::{figure} figs/inverse-filter.svg
:name: F:restoration:inverse-filter
Result of the inverse filter.
:::

The catastrophic result of the inverse filter is due to the fact of approximating the noise to be zero.
Indeed, according to the definition of $\widehat{x}$ and considering $Y = HX + B$:

$$
\widehat{x}
= \mathcal{F}^{-1} \left[ \frac{Y}{H} \right]
= \mathcal{F}^{-1} \left[ X + \frac{B}{H} \right]
= x + \mathcal{F}^{-1} \left[ \frac{B}{H} \right]
$$

This means that the deconvolved image $\widehat{x}$ corresponds to $x$ with an additional term equals to the inverse Fourier transform of $B/H$.
The PSF $H$ being generally a low-pass filter, the values of $H(m,n)$ tend towards $0$ for high frequencies $(m,n)$.
Because $H$ is in the denominator, this tends to drastically amplify the high frequencies of the noise,
and then the term $B/H$ quickly dominates $X$.
This explains the result of @F:restoration:inverse-filter.

One solution consists in considering only the low frequencies of $Y/H$.
This is equivalent to truncating the result given by the inverse filter by cancelling the high frequencies before calculating the inverse Fourier transform.
The result of the deconvolution is much more acceptable, as shown by @F:restoration:truncated-inverse-filter,
although the result is still far from perfect (there are many variations in intensity around objects, such as tree trunks)...

:::{figure} figs/truncated-inverse-filter.svg
:name: F:restoration:truncated-inverse-filter
Result of the truncated inverse filter with very small noise.
The truncation is set so that the restored image is visually the best one.
:::

<!------------------------------------------------------------------------------------------------>

## Wiener Filter

The image restored by the Wiener filter is given by:

$$
\widehat{x} = g * y
$$

where the Wiener filter is defined as

$$
g = \mathcal{F}^{-1} \Bigg[ \frac{H^*}{|H|^2 + K} \Bigg]
$$

and $K$ is a constant set by the user.

The Wiener filter is typically implemented in the Fourier domain, yielding:

$$
\widehat{x} = \mathcal{F}^{-1} \Bigg[ \frac{H^*}{|H|^2 + K} Y \Bigg].
$$
  
<!------------------------------------------------------------------------------------------------>

:::{dropdown} Proof

The Wiener filter, denoted by $g$ and Fourier transform $G$, applies to the observation $y$ such that:

$$
\widehat{x} = g * y
\qquad\Leftrightarrow\qquad
\widehat{X} = GY.
$$

This filter is established in the statistical framework: the image $x$ and the noise $b$ are considered to be random variables.
They are also assumed to be statistically independent.
As a result, the observation $y$ and the estimate $\widehat{x}$ are also random variables.
The calculations are done in the Fourier domain for simplicity, since convolutions become multiplications.

The goal of Wiener filter is to find the image $\widehat{X} = \mathcal{F}[\widehat{x}]$ closest to $X = \mathcal{F}[x]$,
in the sense of the mean squared error $\mathrm{MSE}$.
Thereby :

\begin{align*}
\mathrm{MSE}
&= \mathbb{E}\left[(\widehat{X}-X)^2\right] \\
&= \mathbb{E}\left[(GY-X)^2\right] \\
&= \mathbb{E}\left[\big(G(HX+B)-X\big)^2\right] \\
&= \mathbb{E}\left[\big((GH-I)X+GB\big)^2\right]
\end{align*}

where $I$ is the identity matrix.
Expanding the previous expression yields:

\begin{align*}
\mathrm{MSE} = \mathbb{E}\Big[ &(GH-I)^*(GH-I)X^*X \\
+ &(GH-I)^*GX^*B \\
+ &G^*(GH-I)B^*X \\
+ &G^*GB^*B \Big]
\end{align*}

where $\cdot^*$ denotes the conjugate of a variable.
Since the expectation $\mathbb{E}$ is linear and because only $X$ and $B$ are random variables,
we can write the previous expression into four terms:

\begin{align*}
\mathrm{MSE}
= &   (GH-I)^*(GH-I) \,\mathbb{E}\big[X^*X\big]\\
  & + (GH-I)^*G      \,\mathbb{E}\big[X^*B\big]\\
  & + G^*(GH-I)      \,\mathbb{E}\big[B^*X\big]\\
  & + G^*G           \,\mathbb{E}\big[B^*B\big].
\end{align*}

The covariances $\mathbb{E}\big[X^*B\big]$ and $\mathbb{E}\big[B^*X\big] $ are zeros because $X$ and $B$ are independent.
Moreover, $\mathbb{E}\big[X^*X\big]$ and $\mathbb{E}\big[B^*B\big]$ are the power spectral densities of $x$ and $$b$
(the power spectral density is the expectation of the square of the modulus of the Fourier transform).
The power spectral densities are now denoted:

$$
S_x = \mathbb{E}\big[X^*X\big]
\qquad
S_b = \mathbb{E}\big[B^*B\big].
$$

Then the mean squared error simplifies into:

$$
\mathrm{MSE} = (GH-I)^*(GH-I) S_x + G^*G S_b
$$

We look for the filter $G$ that minimizes the MSE, or equivalently, that cancels the derivative of MSE:

\begin{align*}
                       & \frac{\partial \mathrm{MSE}}{\partial G} = (GH-I)^*H S_x + G^* S_b = 0 \\
  \Leftrightarrow\quad &G^*H^*H S_x - H S_x + G^* S_b = 0  \\
  \Leftrightarrow\quad &G^* ( H^*H S_x + S_b) = H S_x  \\
  \Leftrightarrow\quad &G^* = \frac{H S_x}{H^*H S_x + S_b}  \\
  \Leftrightarrow\quad &G = \frac{H^* S_x}{H^*H S_x + S_b}  \\
  \Leftrightarrow\quad &G = \frac{H^* S_x}{|H|^2 S_x + S_b}
\end{align*}

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

🥳

:::

<!------------------------------------------------------------------------------------------------>

The result of the Wiener filter is illustrated @F:restoration:wiener-filter:
it is clearly much better than the inverse filter, including its truncated variant!

:::{figure} figs/wiener-filter.svg
:name: F:restoration:wiener-filter
Result of Wiener filter
($\lambda$ is set so that the estimation is the best in terms of MSE).
:::

Note that where $H$ vanishes (typically in high frequencies),
the issue of noise amplification observed with the inverse filter is mitigated,
as the constant $K$ in the denominator prevents the denominator to tends to 0.

Moreover, $S_b = 0$ in the absence of noise, so $K$ can be set to zero and the Wiener filter reduces to the inverse filter:

$$
\widehat{x}
= \mathcal{F}^{-1} \Bigg[ \frac{H^*}{|H|^2} Y \Bigg]
= \mathcal{F}^{-1} \Bigg[ \frac{Y}{H} \Bigg].
$$



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
