---
title: "Exercise: A kerosene spill (advection-diffusion)"
---

# Exercise: A Kerosene Spill

Related lessons: [PDE model equations](../../notes/01-pdes-classification-and-model-equations.md) and [the advection equation](../../notes/02-advection-equation-ftbs-ftcs.md).

A tanker truck has an accident and spills 100 kg of kerosene into a river (scenario adapted from Socolofsky and Jirka, 2004). The spill occurs over 3 minutes and can be treated as uniformly distributed across the river cross section. A fish farm has its water intake 2.5 km downstream of the spill.

![Sketch of the kerosene spill problem](figures/kerosene-spill.jpg)

If the river is well mixed across the section, kerosene transport follows the advection-diffusion equation

$$\frac{\partial C}{\partial t}+U\frac{\partial C}{\partial x}=D_L\frac{\partial^2C}{\partial x^2},$$

where $C$ is mass concentration ($\mathrm{kg/m^3}$). For an instantaneous volume source the analytic solution is

$$\frac{C}{C_o}=\frac12\left[\operatorname{erf}\!\left(\frac{x-Ut}{\sqrt{4D_Lt}}\right)-\operatorname{erf}\!\left(\frac{x-L-Ut}{\sqrt{4D_Lt}}\right)\right],$$

where $C_o$ is the initial concentration ($C=C_o$ for $0\le x\le L$ at $t=0$), $D_L$ is the longitudinal dispersion coefficient and $L$ is the initial length of the cloud. Take $L=U\,\Delta t_{spill}$ and $D_L=42\ \mathrm{m^2/s}$. (Choose a reasonable river velocity $U$ and cross-sectional area, and state them.)

1. Using the initial condition and the analytic solution, make two figures:
   1. $C$ vs $x$: the initial distribution and the distribution 2 hours after the accident. From the figure, find the location of the center of mass of the cloud, the maximum concentration in the river and the characteristic width of the cloud at $t=2$ h.
   2. $C$ vs $t$ at the fish farm intake. Will the concentration at the intake ever exceed $1\ \mu\mathrm{g/L}$?
2. Write a finite-difference solver for the 1D advection-diffusion equation using two discretization schemes of your choice. For each:
   - state the truncation error and the general stability conditions;
   - give the specific limits on $\Delta x$ and $\Delta t$ for this problem;
   - show empirically that the stability conditions must be met.
3. Compare the numerical and analytic solutions by plotting the numerical output on the two figures from problem 1. Show how the $t=2$ h solution changes with $\Delta x$. Which discretization is more accurate?
4. Upwind schemes produce numerical diffusion. How close to the analytic solution can you get by solving only the pure advection equation $\partial C/\partial t+U\,\partial C/\partial x=0$ with FTBS? What controls the amount of numerical diffusion?
