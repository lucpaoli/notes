---
layout: default
title: The One Fluid Approximation
parent: The Flash Algorithm
nav_order: 5
math: mathjax3
---
References: Mixing And Combining Rules

# The One Fluid Approximation

This approximation allows you to describe a mixture of fluids using the standard forms of equations of state. To do this you use "mixing rules" to describe the constants, *a, b* for the van der Waals equations, as functions of the constants of the constituent fluids.

From statistical mechanics you can describe exact results for the virial equation for mixtures. The virial coefficients are related to the intermolecular potential between molecules, and for pure fluids they are functions of temperature only.
$$
\begin{align*}
Z &= \frac{Pv}{RT} = 1 + \frac{B}{v} + \frac{C}{v^2} + ... \\
B &= \sum_i \sum_j x_ix_jB_{ij}(T)\\
C &= \sum_i \sum_j \sum_k x_ix_jx_kC_{ijk}(T), etc.
\end{align*}
$$

Since the expressions for $B, C$ are exact results, they can be considered low density boundary conditions that should be satisfied for mixtures by other equations of state when expanded into the virial form.

Currently there is no exact high-density mixture boundary condition, but there is the observation that at liquid densities empirical activity coefficient models such as van Laar, Wilson, UNIQUAC provide a good representation of the excess energy of mixing.


## The Van der Waals Mixing Model

It is not possible to satisfy both the first and second virial coefficients with composition dependence of the $b$ parameter.

If you choose to satisfy the first virial coefficient then:
$$
\begin{align*}
a &= \sum_i\sum_jx_ix_ja_{ij}\\
b &= \sum_i\sum_jx_ix_jb_{ij}
\end{align*}
$$
Where the cross coefficients are given by
$$
\begin{align*}
a_{ij} &= \sqrt{a_{ii}a_{jj}}(1-k_{ij})\\
b_{ij} &= \frac12(b_{ii}+b_{jj})(1-\delta_{ij})
\end{align*}
$$

And $k_{ij}, \delta_{ij}$ are binary interaction parameters. Generally $\delta$ is set to 0, reducing the expression of b to
$$b = \sum_i x_i b_i$$

## Non-Quadratic Combining Rules

By adding additional composition dependence to the $a$ parameter, you can fit the results more accurately to empirical data. However, this does not preserve the theoretically quadratic nature, so do not satisfy any of the boundary conditions discussed.

