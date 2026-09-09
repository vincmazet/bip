(P:digital-images:color-models)=
# Color models

<!-- Rajouter YCbCr ?-->

A *color model*, or *color space*, is a mean to represent colors as points within a specific space.
Several color models exist, some with multiple variations.
This section focuses on the most common color spaces.

<!------------------------------------------------------------------------------------------------>

(P:digital-images:rgb-color-model)=
## The RGB color model

The RGB (red, green, blue) color model uses additive color mixing,
where every colors can be made by combining primary colors (red, green, blue) with the appropriate intensity
(@F:digital-images:additive-mixing).
The RGB color model is used by screens, and, as a consequence, ubiquitous in image processing.

:::{figure} ../src/figs/additive-mixing.svg
:name: F:digital-images:additive-mixing
:width: 30%
Additive color mixing.
:::

The RGB model is based on a 3D Cartesian coordinate system, as seen below.
By convention, the values $R$, $G$ and $B$ are assumed to be in $[0,1]$.
Nevertheless, digital images are generally quantized on 8 bits per band,
thus giving values $R$, $G$, and $B$ to lie on $2^8=256$ values in $\{0,\dots,255\}$.
Therefore a total of $256^3=16\,777\,216$ colors can be generated.

:::{figure} figs/model-rgb.svg
:name: F:digital-images:rgb
:width: 60%
The RGB color space.
:::

A "dual" color model is the CMY (cyan, magenta, yellow) color model.
It is not designed to be used in image processing but rather for color printing since adding pigments on a white surface removes light:
this explained why it uses subtractive color mixing rather than additive color mixing.

<!------------------------------------------------------------------------------------------------>

## The HSV color model

The RGB and CMY models do not directly relate to the human sense of color.
Instead, the HSV (hue, saturation, value) color model corresponds closely with the way humans describe and interpret color.
Indeed, hue corresponds to the type of color (such as orange, cyan or blue),
saturation corresponds to the purity of color,
and value corresponds to the brightness.
In addition to this, the HSV model has the advantage to extract the grayscale information from a color image thanks to the value band,
making it suitable for some grayscale techniques.

The HSV color model is represented by the cylinder, as seen below.

:::{figure} figs/model-hsv.svg
:name: F:digital-images:hsv
:width: 75%
The HSV color space.
:::

The conversion from RGB color model to HSV color model is performed using the following operations,
assuming that the RGB values have been normalised in the range $[0,1]$, hue is in the range $[0,360^{\circ}]$, saturation and value are in the range $[0,1]$:

$$
  H &= H' \,\mathrm{mod}\, 360
  \quad\text{where}\quad
  H' &=
  \begin{cases}
    60 \, (G - B)/\delta               &\text{if } R=V, \\
    60 \, (B - R)/\delta + 120 &\text{if } G=V, \\
    60 \, (R - G)/\delta + 240 &\text{if } B=V, \\
  \end{cases}\\
  S &= \frac{\delta}{V}, \\
  V &= \mathrm{max}(R, G, B),
$$
with $\delta = \mathrm{max}(R, G, B) - \mathrm{min}(R, G, B)$.

The HSV color model has not to be confused with
the HSI (hue, saturation, intensity) and HSL (hue, saturation, luminance) color models
which mainly differ from the HSV color model in the third band.

<!------------------------------------------------------------------------------------------------>

## A color generator

You can use the sliders below to combine the different bands of the previous color models,
and perceive the effect on the color.

Try to find the RGB combination for creating
yellow  <span style="display: inline-block; width: 1em; height: 1em; background: #ffff00; border: 1px solid black; vertical-align: -.2ex;"></span>,
orange  <span style="display: inline-block; width: 1em; height: 1em; background: #ff8000; border: 1px solid black; vertical-align: -.2ex;"></span>,
purple  <span style="display: inline-block; width: 1em; height: 1em; background: #ff00ff; border: 1px solid black; vertical-align: -.2ex;"></span>,
or cyan <span style="display: inline-block; width: 1em; height: 1em; background: #00ffff; border: 1px solid black; vertical-align: -.2ex;"></span> !

<iframe src="https://vincmazet.github.io/spetsi/standalone/color-generator.html" style="padding-bottom:250px"><a href="https://vincmazet.github.io/spetsi/standalone/color-generator.html">Animation</a></iframe>