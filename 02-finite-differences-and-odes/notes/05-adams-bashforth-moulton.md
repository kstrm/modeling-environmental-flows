---
title: Multistep Methods - Adams-Bashforth-Moulton
---

# Multistep Methods: Adams–Bashforth–Moulton

:::{admonition} Learning objectives
:class: tip
After this lesson you should be able to:

- contrast multistep methods with Runge–Kutta methods
- distinguish Adams–Bashforth (explicit) from Adams–Moulton (implicit)
- explain why higher-order multistep methods are not self-starting
:::

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

## Check your understanding

**1.** How does a multistep method differ from Runge–Kutta?

:::{dropdown} Answer
A multistep method reuses slopes from previous grid points. Runge–Kutta uses only step $i$ and makes extra slope evaluations inside the step.
:::

**2.** Why are higher-order multistep methods not self-starting, and what is the usual fix?

:::{dropdown} Answer
They need several previous values, but initially only one is known. The first few points are generated with a single-step method such as RK4.
:::

**3.** Which is explicit and which implicit, and what is the one-step Adams–Moulton method?

:::{dropdown} Answer
Adams–Bashforth is explicit; Adams–Moulton is implicit. The one-step Adams–Moulton method is the trapezoidal rule, called Crank–Nicolson when applied to PDEs.
:::
