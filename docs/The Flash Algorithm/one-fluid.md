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
\begin{aligned}
Z &= \frac{Pv}{RT} = 1 + \frac{B}{v} + \frac{C}{v^2} + ... \\
B &= \sum_i \sum_j x_ix_jB_{ij}(T)\\
C &= \sum_i \sum_j \sum_k x_ix_jx_kC_{ijk}(T), etc.
\end{aligned}
$$

Since the expressions for $B, C$ are exact results, they can be considered low density boundary conditions that should be satisfied for mixtures by other equations of state when expanded into the virial form.

Currently there is no exact high-density mixture boundary condition, but there is the observation that at liquid densities empirical activity coefficient models such as van Laar, Wilson, UNIQUAC provide a good representation of the excess energy of mixing.


## The Van der Waals Mixing Model

It is not possible to satisfy both the first and second virial coefficients with composition dependence of the $b$ parameter.

If you choose to satisfy the first virial coefficient then:


$$ \begin{aligned}
a &= \sum_i\sum_jx_ix_ja_{ij}\\
b &= \sum_i\sum_jx_ix_jb_{ij}
\end{aligned} $$


Where the cross coefficients are given by


$$\begin{aligned}
a_{ij} &= \sqrt{a_{ii}a_{jj}}(1-k_{ij})\\
b_{ij} &= \frac12(b_{ii}+b_{jj})(1-\delta_{ij})
\end{aligned}$$


And $k_{ij}, \delta_{ij}$ are binary interaction parameters. Generally $\delta$ is set to 0, reducing the expression of b to
$$b = \sum_i x_i b_i$$

## Non-Quadratic Combining Rules

By adding additional composition dependence to the $a$ parameter, you can fit the results more accurately to empirical data. However, this does not preserve the theoretically quadratic nature, so do not satisfy any of the boundary conditions discussed.

## Wong-Sandler Mixing Rules

Introduced in [Wong 1992](https://doi.org/10.1002/aic.690380505) and reformulated in [Orbey 1995](https://doi.org/10.1002/aic.690410325) to eliminate a parameter and smooth the transition
()

- Equates the excess Helmholtz free energy at infinite pressure from an equation of state to that from an activity coefficient model
- This insures the second virial coefficient has a quadratic composition dependence
- In the reformulation, the parameters can be obtained from vapour-liquid equilibrium data or from the two infinite dilution activity coefficients for each binary pair in the mixture
- When estimated from the UNIFAC group contribution model, the mixing rule becomes entirely predictive

### Wong-Sandler equations:

$$
\begin{aligned}
b_m &= \frac{\sum\sum x_i x_j\left(b-\frac{a}{RT}\right)}{1-\frac{A^E}{CRT}-\sum x_i \frac{a_i}{RTb_i}}\\
\frac{a_m}{b_m} &= \sum x_i \frac{a_i}{b_i} + \frac{A^E}{C}\\
\text{Which can be}&\text{ written as}\\
b_m - \frac{a_m}{RT} &= \sum \sum x_i x_j\left(b-\frac{a}{RT}\right)_{ij}\\
\frac{A^E}{C}&=\frac{a_m}{b_m}-\sum x_i\frac{a_i}{b_i}
\end{aligned}
$$

$$
\begin{aligned}
\left(b-\frac{a}{RT}\right)_{ij} &= \frac12\left[\left(b-\frac{a}{RT}\right)_i+\left(b-\frac{a}{RT}\right)_j\right](1-k_{ij})
\end{aligned}
$$

Where $C$ is a constant depending on the equation of state, $-0.62323$ for the modified PR used in Orbey.

A key advantage of these mixing rules is that in a mixture it's likely that only some binary pairs form highly nonideal mixtures requiring complex mixing rules, while other's in the same mixture can be described by the classical vdW mixing rule, so it's advantageous to select a set of equations that can reduce to the vdW rule.

### Reformulation
This preserves the same basic equations, but rewrites the cross second virial term as
$$
\left(b-\frac{a}{RT}\right)_{ij} = \frac12(b_i+b_j)-\frac{\sqrt{a_i}a_j(1-k_{ij})}{RT}$$

When using this rule, if you set $\tau_{ij}=0$, you recover the van der waals mixing rules for the case where 

$$ k_{ij} = 1 - \frac{1}{2\sqrt{a_ia_j}}\left[a_i\frac{b_j}{b_i}+a_j\frac{b_i}{b_j} + \frac{RT}{C}(b_i\tau_{ij}+b_{j}\tau_{ji})\right] \tag{1}$$

This is not particularly useful, as it means you can't use fitted parameters for that mixing rule from other people. You can rearrange Eq. (1) to (2) and use along with (3) to obtain 2 values of $\tau$ for each binary pair for when you want to obtain the classic mixing rule for more ideal mixtures.

$$\tau_{ij} = \left(\left[(1 - k_{ij})\cdot 2\sqrt{a_ia_j} - a_i\frac{b_j}{b_i} - a_j\frac{b_i}{b_j}\right]\cdot\frac{C}{RT} - b_j\tau_{ji}\right)/b_i \tag{2} $$
$$ \tau_{ji} = \frac{C}{RT}\left[\frac{\sqrt{a_ia_j}(1-k_{ij})}{b_{ij}} - \frac{a_i}{b_j}\right] \tag{3} $$

Another method is possible, where you determine $\tau_{ji}, \tau_{ij}$ from activity coefficients produced by a predictive model such as UNIFAC by solving Eq. (4) simultaneously for both values.
$$\tau_{ji} = \ln\gamma_i^\infty - \tau_{ij}\frac{b_i}{b_j}\exp(-\alpha_{ij}\tau_{ij}) \tag{4}$$

The overall approach is:


| Ideal mixture                        | Nonideal mixture                                         |
|--------------------------------------|----------------------------------------------------------|
| $\alpha_{ij} = \alpha_{ji} = 0$      | $\alpha_{ij} = \alpha_{ji} = 0.1$                        |
| $k_{ij}$ regressed                   | $k_{ij} = 0$                                             |
| $\tau_{ij}$ calculated from (2), (3) | $\tau_{ij}$ regressed or obtained from UNIFAC prediction |


When regressing $\tau$, temperature dependence is always included, the simplest of which is $\tau = g/T$, where $g$ is the interaction energy for that binary pair.
More complex temperature dependence does exist but whatever formulation used, the general approach is to fit $\tau$ individually to isotherms and consider temperature dependence after.



