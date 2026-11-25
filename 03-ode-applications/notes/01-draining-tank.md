---
title: Example - Draining a Tank
---

# Example: Draining a Tank

A tank of diameter $D$ has a drain of diameter $d$ at the bottom. We want the water depth $h=h(t)$ and the time to drain. This is an **unsteady** problem, different from the typical steady problems in an undergraduate course.

Companion notebook: [4th-order Runge–Kutta, tank example](../completed/04_4th-Order_Runge-Kutta_TankExample.ipynb).

![Draining tank and well-mixed tank schematics](../figures/tank-schematics.svg)

*Figure: A draining tank (left) and a well-mixed tank carrying a dissolved substance (right).*

## Governing equation

Conservation of mass for the water in the tank, $dM/dt=\sum\dot m_{in}-\sum\dot m_{out}$, with $M=\rho\mathcal V$ and $\dot m=\rho Q$ ($Q$ is the volumetric flow rate):

$$\frac{d}{dt}(\rho A_1h)=\rho Q_{in}-\rho A_2V_2.$$

Since $A_1$ and $\rho$ do not depend on time,

$$\frac{dh}{dt}=\frac1{A_1}\left(Q_{in}-A_2V_2\right).$$

Note that $V_2=f(h)$ and $h=h(t)$, so we need a relationship between the exit velocity and the depth.

## Closure

Apply the energy (Bernoulli) equation from the free surface (1) to the drain exit (2), with $p_1=p_2=0$ (atmospheric), negligible head loss $h_L\approx0$ and $V_1\ll V_2$:

$$\frac{V_2^2}{2g}=z_1-z_2=h\;\Rightarrow\;V_2=\sqrt{2gh}.$$

This is a *closure model*: it supplies the missing relationship. With $A_1=\pi D^2/4$ and $A_2=\pi d^2/4$,

$$\boxed{\frac{dh}{dt}=\frac{4}{\pi D^2}\left(Q_{in}-\frac{\pi d^2}{4}\sqrt{2gh}\right)}$$

Can we solve it? And how will we know whether we implemented the numerical method correctly?

## Analytic solution for pure draining ($Q_{in}=0$)

$$\frac{dh}{dt}=-\frac{d^2}{D^2}\sqrt{2gh}\;\Rightarrow\;\int h^{-1/2}\,dh=-\frac{d^2}{D^2}\sqrt{2g}\int dt,$$

$$2h^{1/2}=-\frac{d^2}{D^2}\sqrt{2g}\,t+C_1\;\Rightarrow\;h^{1/2}=-\frac{d^2}{D^2}\sqrt{\frac g2}\,t+C_2.$$

With the initial condition $h=h_0$ at $t=0$, $C_2=h_0^{1/2}$:

$$h(t)=\left[h_0^{1/2}-\frac{d^2}{D^2}\sqrt{\frac g2}\;t\right]^2.$$

Setting $h=0$ gives the drain time,

$$t_{drain}=\frac{D^2}{d^2}\sqrt{\frac{2h_0}{g}}.$$

## Numerical solution

The equation has the form $dh/dt=g(h)$ with $g(h)=-\dfrac{d^2}{D^2}\sqrt{2gh}$. Solve it with 4th-order Runge–Kutta (see the [Runge–Kutta note](../../02-finite-differences-and-odes/notes/03-runge-kutta-methods.md)) and compare with the analytic solution above, which provides the check on the implementation.

## A note on the end of the run

With $D=3$, $d=1/12$, $h_0=3$ (consistent units, e.g. ft) and $\Delta t=60$ s, the analytic drain time is about 9.3 min. If the run is carried past that time, the numerical solution produces `nan` and a `RuntimeWarning: invalid value encountered in sqrt`, because $h$ becomes slightly negative and $\sqrt{2gh}$ is undefined. (The analytic expression, being a square, would climb back up, which is unphysical.) The fix is to stop the loop once the depth is effectively zero, e.g. `if y[i+1] <= 0.001*y0: break`, and report the time at which that happened.
