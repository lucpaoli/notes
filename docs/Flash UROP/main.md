---
layout: default
title: Flash UROP
nav_order: 1
math: mathjax3
has_children: true
---

# The Flash Problem
A common problem in chemical engineering is the flash problem, determining the vapour and liquid compositions for an overall composition, i.e. the feed composition, and the current state.
The state can be specified with any combo of thermodynamic variables. It is often formulated as *T, P* or an "Isothermal Flash", or as *H, P* an "Isenthalpic Flash"

It appears most obviously in flash drums or distillation columns, but it also occurs in compositional reservoir simulations, requiring a flash at each grid block for every time step.

This is only ever a problem when dealing with mixtures, as clearly for a pure substance the liquid and vapour will both be pure.

The flash problem is solved numerically, generally as either a gibbs energy minimisation problem, or with successive substitution of the composition variables.

$$
\min \text{g} = \sum_{i=1}^N y_i \mu_i^{\scriptsize V} + x_i \mu_i^{\scriptsize L} $$

There are 2 key equations that are solved iteratively, the chosen equation of state and the Rachford-Rice equation.

### The Rachford-Rice equation

The Rachford-Rice equation has at most one solution for $\beta$ that guaranties all $x_i, y_i$ are positive. It is easy and efficient to use a step limited Newton-Raphson method to solve this, as the derivative is easy to obtain analytically.
$$\sum_i \frac{z_i(K_i-1)}{1+\beta(K_i-1)} = 0\\
h(\beta) = \sum_{i=1}^N \frac{K_i - 1}{(K_i-1)\beta + 1}\\
h'(\beta) = - \sum_{i=1}^N \left(\frac{K_i - 1}{(K_i-1)\beta + 1}\right)^2z_i \\
\beta_{k+1} = \beta_k - \frac{h}{h'}$$

Checking each iteration if $\beta_{k+1}$ exceeds a defined $\beta_{max}, \beta_{min}$. These maximum and minimum values can either be described in terms of your component equilibrium constants, or as $[0, 1]$. The former is known as the "negative flash" procedure, and is described in [Curtis, 1989](http://dx.doi.org/10.1016/0378-3812(89)80072-X). It allows for calculations of equilibrium compositions for systems that physically exist as a single phase, and corresponds to a saddle point in the Gibbs energy surface. It is an important tool when used in the inner $\beta$ loop in a larger iterative flash procedure. 

Once this is solved, $\vec{x}, \vec{y}$ can be calculated as:
$$\begin{align*} x_i &= \dfrac{z_i}{1+\beta(K_i-1)}\\ y_i &= K_i x_i \end{align*}$$

### The Equation of State

Any equation of state that can capture the two phase region can be used, e.g. Peng-Robinson, Redlich-Kwong. A complex equation of state can be used, but I am not familiar with the process.

Generally, you just need to be able to evaluate the component fugacities and the overall Gibbs free energy for a given composition. This allows you to check for equilibrium, where the component fugacities are equal, as well as being the basis for most numerical methods.


