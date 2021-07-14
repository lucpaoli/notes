---
layout: default
title: Numerical Methods 
parent: Flash UROP
nav_order: 2
math: mathjax3
---

# Numerical Methods in Flash Problems

## Successive substitution
The most basic method of solving a flash problem is by successive substitution of variables, either \(K_i\) component equilibrium variables, or \(x_i, y_i\) composition variables.

Interestingly this has been shown to be a form of gradient descent. This is described in [Ammar 1987](https://doi.org/10.1002/aic.690330606).

## Acceleration steps
Honestly, I haven't been able to get any acceleration methods to work. Successive substitution works really well and I have been unable to improve it. 

Newton's method is effective in a small neighbourhood of the solution, having quadratic convergence. It can be calculated 

