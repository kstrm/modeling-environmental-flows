---
title: The Advection Equation - FTBS and FTCS
---

# The Advection Equation: FTBS and FTCS

Companion notebook: [Simple PDE: advection](../completed/13_SimplePDE_Advection.ipynb).

## Problem

$$\frac{\partial u}{\partial t}=-c\frac{\partial u}{\partial x},\qquad u(x,0)=f(x).$$

The exact solution is $u(x,t)=f(x-ct)$: the initial profile translates at speed $c$ (a moving frame of reference). We need one boundary condition (the inflow end).

## Step 1: Discretize the domain

A grid in space and time: $x_i=i\,\Delta x$ and $t_n=n\,\Delta t$, with unknowns $u_{i,n}$ (or $u_i^n$).

## Step 2: Discretize the governing equation

Pick a scheme for space and time.

**FTBS (forward in time, backward in space)**

$$\frac{\partial u}{\partial t}\approx\frac{u_{i,n+1}-u_{i,n}}{\Delta t}+O(\Delta t),\qquad\frac{\partial u}{\partial x}\approx\frac{u_{i,n}-u_{i-1,n}}{\Delta x}+O(\Delta x),$$

so

$$\frac{u_{i,n+1}-u_{i,n}}{\Delta t}=-c\,\frac{u_{i,n}-u_{i-1,n}}{\Delta x}\;\Rightarrow\;u_{i,n+1}=u_{i,n}-\frac{c\,\Delta t}{\Delta x}\left(u_{i,n}-u_{i-1,n}\right).$$

The stencil has 2 points on 2 time levels. Given the initial condition $u_{i,0}$, step through $n=1,2,\ldots$ (the boundary values are needed at each new level).

**FTCS (forward in time, central in space)**

$$\frac{\partial u}{\partial x}\approx\frac{u_{i+1,n}-u_{i-1,n}}{2\Delta x}+O(\Delta x^2)\;\Rightarrow\;u_{i,n+1}=u_{i,n}-\frac{c\,\Delta t}{2\Delta x}\left(u_{i+1,n}-u_{i-1,n}\right).$$

The stencil has 3 points on 2 time levels.

## Numerical experiment

Initial condition (square wave) on $x\in(0,2)$, with $u=1$ at $x=0$:

$$u(x,0)=\begin{cases}2&0.5\le x\le1\\1&\text{elsewhere.}\end{cases}$$

Set up with $c=1$, $n_x=50$ points and $\Delta t=0.02$. Examine pure (conservative) advection with both schemes.

```python
import numpy as np
import matplotlib.pyplot as plt

xstart, xend, nx = 0, 2, 50
dt, c = 0.02, 1
dx = (xend - xstart) / (nx - 1)
x = np.linspace(xstart, xend, nx)

u0 = np.ones(nx)
u0[np.intersect1d(np.where(x >= 0.5), np.where(x <= 1))] = 2

# FTBS
u = u0.copy()
for n in range(1, 25):
    un = u.copy()
    for i in range(1, nx):
        u[i] = un[i] - c*dt/dx*(un[i] - un[i-1])

# FTCS
u = u0.copy()
for n in range(1, 25):
    un = u.copy()
    for i in range(1, nx - 1):
        u[i] = un[i] - c*dt/(2*dx)*(un[i+1] - un[i-1])
```

### A vectorized version

The double loop is the clearest way to see the scheme, but NumPy can update every grid point of one time step in a single array operation. Slicing does the work: `un[1:]` holds the $u_i$ and `un[:-1]` holds the $u_{i-1}$.

```python
# FTBS, vectorized in space (the loop over time stays)
u = u0.copy()
for n in range(1, 25):
    un = u.copy()
    u[1:] = un[1:] - c*dt/dx*(un[1:] - un[:-1])

# FTCS, vectorized in space
u = u0.copy()
for n in range(1, 25):
    un = u.copy()
    u[1:-1] = un[1:-1] - c*dt/(2*dx)*(un[2:] - un[:-2])
```

These give the same numbers as the loops (check with `np.allclose`) and are roughly 10 to 100 times faster, more so on finer grids. The time loop cannot be vectorized because each step needs the one before it. The companion notebook times both versions.

**Observations**

- **FTBS** after 25 steps ($t=0.5$): the square wave has moved to the right by about the right amount, but the sharp edges are smeared. The scheme is stable here but numerically *diffusive*, behaving as though a diffusion term had been added. Compare with the analytic solution (the initial profile shifted by $ct$).
- With a periodic boundary condition (`u[0] = u[-1]`) run for a long time (75 steps, $t=1.5$), the profile is smeared further into a smooth bump that wraps around the domain.
- **FTCS** is more accurate in space (second order) but, run for the same time, produces large growing oscillations (values below 0 and above 3 for a wave that should stay between 1 and 2). The scheme is unstable for this equation, however small the time step. Accuracy in space alone is not enough: the combination of time and space schemes determines stability.

This motivates asking: *Other methods?* The next two notes explain why FTCS fails and FTBS smears ([stability and the CFL condition](03-stability-cfl-and-von-neumann.md)) and introduce the alternatives ([upwind, Lax and implicit schemes](04-upwind-lax-and-implicit-schemes.md)).
