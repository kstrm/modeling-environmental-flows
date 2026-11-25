---
title: Multistep Methods - Adams-Bashforth-Moulton
---

# Multistep Methods: Adams–Bashforth–Moulton

Multistep methods use information from previous grid points to advance to $i+1$, in contrast to Runge–Kutta methods, which use only information at step $i$ (with extra evaluations inside the step).

- **Adams–Bashforth** (explicit): uses slopes already computed at $i,\,i-1,\,i-2,\ldots$
- **Adams–Moulton** (implicit): also uses the unknown slope at $i+1$ (and, for higher order, earlier points). The one-step Adams–Moulton method is the trapezoidal rule, known as Crank–Nicolson when applied to PDEs.

## Idea

Fit a polynomial through the points you have already computed and integrate the fit across the step:

$$y_{i+1}=y_i+\int_{t_i}^{t_{i+1}}f(y,t)\,dt\;\approx\;y_i+\int_{t_i}^{t_{i+1}}p(t)\,dt,$$

where $p(t)$ is the fitted polynomial.

## Main difficulty

Higher-order multistep methods are **not self-starting**: they need more data than a single starting value at $i$. A common remedy is to generate the first few points with a single-step method such as RK4.

## Assignment

Read up on the Adams–Bashforth method, be ready to teach it, and compare it to Runge–Kutta.
