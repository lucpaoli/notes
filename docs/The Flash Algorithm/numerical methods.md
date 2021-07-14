---
layout: default
title: Numerical Methods 
parent: The Flash Algorithm
nav_order: 2
math: mathjax3
---

# Numerical Methods in Flash Problems

## Successive substitution
The most basic method of solving a flash problem is by successive substitution of variables, either $K_i$ component equilibrium variables, or $x_i, y_i$ composition variables.

The basic implementation involves calculating the liquid and vapour fugacities from an initial guess of the compositions, then writing the expression for the compositions from the material balance and definition of the equilibrium constant.

$$
\begin{align*}
K_i &= \frac{\phi_i^L(x)}{\phi_i^V(y)}\\
x_{i,k+1} &= \frac{z_i}{1+\beta(K_i-1)}\\
y_{i, k+1} &= \frac{z_i}{1+\beta(K_i-1)}\\
\end{align*}
$$

Interestingly this has been shown to be a form of gradient descent. This is described in [Ammar 1987](https://doi.org/10.1002/aic.690330606).



## Acceleration steps

Newton's method is effective in a small neighbourhood of the solution, having quadratic convergence. 

