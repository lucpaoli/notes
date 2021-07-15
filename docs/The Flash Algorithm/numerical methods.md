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

### Substitution algorithm:
$$
\begin{align*}
K_i &= \frac{\phi_i^L(x)}{\phi_i^V(y)}\\
x_{i,k+1} &= \frac{z_i}{1+\beta(K_i-1)}\\
y_{i, k+1} &= \frac{z_i}{1+\beta(K_i-1)}\\
\end{align*}
$$

Interestingly this has been shown to be a form of gradient descent. This is described in [Ammar 1987](https://doi.org/10.1002/aic.690330606). The Jacobian can be calculated analytically, and the Hessian semi-analytically, in terms of the residual Gibbs energy with respect to the mole number.

$$
\begin{align*}
\nabla g &= \frac{\partial g}{\partial v_i} = \ln\left(\frac{y_i\phi_i^V}{x_i\phi_i^L}\right)\\~\\
\nabla^2 g &= \mathbf{A} + \mathbf{Q}\\~\\
\mathbf{A} &= \frac{1}{\beta(1-\beta)}\left(-1 + \delta_{ij}\frac{z_i}{x_iy_i}\right)\\~\\
\mathbf{Q} &= \frac{\partial \ln \phi+i^V}{\partial v_j} + \frac{\partial \ln \phi_i^L}{\partial l_j}
\end{align*}
$$

where $\delta_{ij}$ is the [kronecker delta](https://en.wikipedia.org/wiki/Kronecker_delta), and the mole numbers $\beta = \sum_i^N v_i$

### Gradient algorithm:


1.  Start with $\ln K$
2.  Solve the Rachford-Rice equation
3. Compute $\vec{x}, \vec{y}$
4.  Calculated the residual gibbs energy
5.  Define 

    $\ln K_{k+1} = \ln K_k - \lambda \Delta g$
    
    where $\lambda$ is parameter that can be calculated through a line search.



## Acceleration steps

Newton's method is effective in a small neighbourhood of the solution, having quadratic convergence. 

