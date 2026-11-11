(P:registration:metric)=
# Similarity metric


Applying the transformation parameterized by its parameters $\theta$ on the source image $f$ yields the transformed image $f'$.
The similarity metric $E(\theta)$ measures the distance (in a mathematical sense) between the reference image $g$ and the transformed image $f'$.
Optimal registration between $g$ and $f'$ is achieved when $E(\theta)$ reaches its minimum.

Thus, the goal of registration reduces to an optimization problem to find the parameters $\theta$ that minimize the similarity metric $E(\theta)$.

The choice of $E$ depends on the feature matching approach.

<!------------------------------------------------------------------------------------------------>

## Definition of the metric

### Intensity-based approach

In the case of an intensity-based (iconic) approach,
a so-called *dense* similarity criterion is used.

There exist several assumptions regarding the relationships between the intensities of the two images.
In the simplest case, it is assumed that pixel intensities are equal, up to additive Gaussian noise.
Therefore, the similarity criterion can be the Euclidean distance between the two images:

$$
  E(\theta) = \sum_{m=1}^M \sum_{n=1}^N \big(f'(m,n) - g(m,n)\big)^2
$$

As we will see in @P:restoration:intro, this metric is also called mean squared error (MSE).


### Feature-based approach

In the case of a feature-based (geometric) approach, a distance between the features is used.

For example, if the features are specific pixels (*e.g.* corners),
the distance between these pixels can be calculated using the Euclidean norm:
$$
  E(\theta) = \sum_{n=1}^N (x_n-x'_n)^2 + (y_n-y'_n)^2
$$
where $(x_n,y_n)$ and $(x'_n,y'_n)$ are the coordinates of the paired pixels.

<!------------------------------------------------------------------------------------------------>

## Optimisation of the metric

As previously mentioned, the goal is to find the transformation parameters ​​$\theta$ that minimize $E(\theta)$.
Mathematically, the problem is expressed as follows:
$$
  \hat{\theta} = \arg \min_{\theta} E(\theta)
$$

@F:registration:optimization-principle illustrates the principle of mathematical optimization.

:::{figure} figs/optimization.png
:height: 250px
:name: F:registration:optimization-principle
Principle of mathematical optimization.
In this example, $E$ is a function of only one parameter: the rotation angle $\theta = \alpha$.
:::

There is a wide variety of optimization methods, but their detailed description lies beyond the scope of this course:
* explicit solution is possible when the mathematical derivative of $E$ can be computed and equated to zero,
* exhaustive search tests all possible solutions (typically implemented via a loop),
* deterministic methods, such as gradient descent, simplex algorithm, or Levenberg-Marquardt algorithm.
* stochastic methods, such as simulated annealing, genetic algorithms, or stochastic gradient.

These optimization methods can be combined with hierarchical schemes (often referred to as "coarse-to-fine" approaches):
the core idea is to decompose the original problem into several smaller, less complex subproblems.
This tends to reduce the risk of converging to a local minimum and accelerates computation.
For instance, a multi-resolution approach can be employed:
the optimization starts on a downsampled image, then it is refined at scales progressively closer to the original image resolution.
Otherwise, the optimization can begin by optimizing a simple deformation model (rigid deformation) then gradually increase its complexity.