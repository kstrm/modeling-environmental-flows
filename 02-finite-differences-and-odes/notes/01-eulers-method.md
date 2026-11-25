---
title: Introduction to Numerical Methods - Euler's Method
---

# Introduction to Numerical Methods: Euler's Method

:::{admonition} Learning objectives
:class: tip
After this lesson you should be able to:

- write the explicit and implicit Euler steps for $dy/dx=f(x,y)$
- interpret an Euler step as moving along a line with the local slope
- say when Euler's method is exact and when it is only an approximation
:::

Reference: any calculus or numerical methods text, or Section 3.2 of Aref and Balachandar (2018).

## Idea

Consider the first-order ODE

$$\frac{dy}{dx}=f(x,y).$$

Rather than integrating analytically, take a finite step:

$$dy=f(x,y)\,dx\;\rightarrow\;\Delta y=f(x,y)\,\Delta x\;\rightarrow\;y_2-y_1=f(x,y)\,(x_2-x_1),$$

$$y_2=y_1+f(x,y)\,(x_2-x_1).$$

Notes:

1. $f(x,y)$ is the slope of $y$ with respect to $x$.
2. New value = old value + slope × step size.
3. This is the equation of a line, $y_2-y_1=m\,(x_2-x_1)$ with $m=f(x_1,y_1)$.
4. It is only the true solution for a line (constant slope). Otherwise it is an approximation whose quality depends on the step size.

## Explicit and implicit versions

Euler's method is the simplest method for integrating an ODE. There are two versions, written here with step size $\Delta x$ (often called $h$).

**Explicit:** the slope is evaluated with information at step $i$ only,

$$y_{i+1}=y_i+f(x_i,y_i)\,\Delta x.$$

This is what we just derived.

**Implicit:** the slope is evaluated with information at the next step, so $y_{i+1}$ appears on both sides,

$$y_{i+1}=y_i+f(x_{i+1},y_{i+1})\,\Delta x.$$

An implicit step generally requires solving an algebraic equation for $y_{i+1}$.

## Alternate notation

Aref and Balachandar write the problem as

$$\frac{d\xi}{dt}=g(\xi,t),\qquad \xi_{i+1}=\xi_i+g(\xi_i,t_i)\,\Delta t,$$

where $\xi$ plays the role of $x_i$ and $\Delta t$ is the time step. Evaluating $g$ at step $i$ is explicit; at $i+1$ is implicit. In time, the slope $d\xi/dt$ at any point sets the direction of the next step.

## Example

Use Euler's method to numerically integrate

$$\frac{d\xi}{dt}=-2t^3+12t^2-20t+8.5=g(t).$$

Explicit Euler gives

$$\xi_{i+1}=\xi_i+\left(-2t_i^3+12t_i^2-20t_i+8.5\right)\Delta t.$$

What else is needed to solve it?

1. Initial condition: $\xi(t_0)=\xi_0=1$.
2. Step size: $\Delta t=0.5$.
3. Start and stop times: $t=0$ to $t=5$.

Compare with the analytic solution, which satisfies the same initial condition:

$$\xi(t)=-\frac{2}{4}t^4+\frac{12}{3}t^3-\frac{20}{2}t^2+8.5\,t+1.$$

Work through this in the notebook [Euler method](../completed/01_Euler_Method.ipynb).

## Check your understanding

**1.** Write one explicit Euler step for $dy/dx=f(x,y)$.

:::{dropdown} Answer
$y_{i+1}=y_i+f(x_i,y_i)\,\Delta x$: the new value is the old value plus the slope times the step.
:::

**2.** When does explicit Euler give the exact solution?

:::{dropdown} Answer
When the slope is constant, i.e. the true solution is a straight line. Otherwise it is an approximation whose quality depends on the step size.
:::

**3.** What is the difference between explicit and implicit Euler?

:::{dropdown} Answer
Explicit evaluates the slope at step $i$; implicit evaluates it at step $i+1$, so $y_{i+1}$ appears on both sides and generally requires solving an algebraic equation.
:::

**4.** Take one step for $d\xi/dt=-2t^3+12t^2-20t+8.5$ with $\xi(0)=1$ and $\Delta t=0.5$. How far is the result from the analytic value?

:::{dropdown} Answer
The slope at $t=0$ is $8.5$, so $\xi(0.5)\approx1+8.5(0.5)=5.25$. The analytic solution gives $1+8.5(0.5)-10(0.25)+4(0.125)-0.5(0.0625)=3.21875$, so one step is off by about $2$. The slope changes a lot over the step.
:::
