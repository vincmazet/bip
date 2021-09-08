# Filtering

The operation of filtering consists in selecting some frequencies in the images.
Especially, we distinguish low-pass filtering which preserves only the low frequencies ({numref}`F:fourier:lowpass`)
and high-pass filtering which preserves only the high frequencies ({numref}`F:fourier:highpass`).

```{figure} lowpass.svg
:name: "F:lowpass"

Example of low-pass filtering: only the low frequencies are kept.
Top row: spatial domain, bottom row: amplitude of the DFT.
```

```{figure} highpass.svg
:name: "F:highpass"

Example of high-pass filtering: only the high frequencies (i.e. the sudden changes in the intensities) are kept.
```

<!-- Filters (low-pass/blur, High-pass/sharp, citer "kernel", lien vers détection de contour) -->