---
title: Boundary Value ODEs - The Shooting Method and the Blasius Boundary Layer
---

# The Shooting Method and the Blasius Boundary Layer

Companion notebook: [Blasius boundary layer](../completed/12_BCproblem_Blasius.ipynb).

## Problem

For a laminar boundary layer over a flat plate, the velocity $u=u(x,z)$ approaches the free-stream value $U_\infty$ at the edge of the layer $\delta$. The governing equations are continuity and the boundary layer momentum equation:

$$\frac{\partial u}{\partial x}+\frac{\partial w}{\partial z}=0,\qquad u\frac{\partial u}{\partial x}+w\frac{\partial u}{\partial z}=\nu\frac{\partial^2u}{\partial z^2}.$$

These admit a **similarity solution**. With the similarity variable

$$\eta=\frac{z}{\sqrt{\nu x/U_\infty}},$$

all velocity profiles (at any $x$) can be expressed in terms of $\eta$, and the PDE collapses to the third-order, nonlinear ODE

$$f'''+\tfrac12ff''=0,\qquad f=f(\eta),\quad u=U_\infty f'(\eta).$$

(The notebook uses the equivalent $y$-based notation $\eta$, $f$, $g$, $h$.) The boundary conditions $u(x,0)=0$ and $u(x,\delta)=U_\infty$ become

$$f(0)=0,\qquad f'(0)=0,\qquad f'(\eta\to\infty)\to1.$$

## Decompose into first-order equations

Let $f'=g$ and $g'=h$ (so $h=f''$). Then $h'=f'''=-\tfrac12ff''=-\tfrac12fh$:

$$f'=g,\qquad g'=h,\qquad h'=-\tfrac12fh,$$

with initial conditions $f(0)=0$ and $g(0)=0$. The third condition is a far-field condition, $g(\eta\to\infty)\to1$, which is awkward to enforce, and there is no initial condition for $h(0)=f''(0)$. This is the difficulty of a boundary value problem.

## Shooting

1. **Guess** a value for $h(0)$ (try $h(0)=1$ first).
2. Integrate the system as an initial value problem with RK4 out to a large $\eta$ (say 10).
3. **Check** whether $g(\eta_\infty)\to1$. If not, update $h(0)$ and repeat.

Define a difference function

$$\phi(h_0^k)=g_k(\eta_\infty;h_0^k)-1,$$

where $k$ is the iteration index. Given $h_0^k$ and $h_0^{k-1}$, a new guess comes from the secant method:

$$h_0^{k+1}=h_0^k+\Delta h_0,\qquad\Delta h_0=-\phi(h_0^k)\left[\frac{h_0^k-h_0^{k-1}}{\phi(h_0^k)-\phi(h_0^{k-1})}\right].$$

Keep updating until $\phi(h_0^k)\approx0$.

## Implementation

The right-hand side returns the three slopes, and the RK4 loop is the array version used for systems of ODEs:

```python
import numpy as np

def f(eta, y):                         # y = [f, g, h]
    return np.array([y[1], y[2], -0.5*y[0]*y[2]])

def blasius(eta, y, f0, g0, h0, delta):
    y[:, 0] = [f0, g0, h0]
    for i in range(len(eta) - 1):
        K1 = f(eta[i],             y[:, i])
        K2 = f(eta[i] + 0.5*delta, y[:, i] + 0.5*delta*K1)
        K3 = f(eta[i] + 0.5*delta, y[:, i] + 0.5*delta*K2)
        K4 = f(eta[i] + delta,     y[:, i] + delta*K3)
        y[:, i+1] = y[:, i] + (delta/6)*(K1 + 2*K2 + 2*K3 + K4)
    return y

def diff(h0, target=1.0):
    return blasius(eta, y, 0, 0, h0, delta)[1, -1] - target

h01, h02, tol = 0.0, 1.0, 1e-4
err = abs(diff(h02))
while err > tol:
    d1, d2 = diff(h01), diff(h02)
    dh = -d2 * (h02 - h01) / (d2 - d1)
    h01, h02 = h02, h02 + dh
    err = abs(diff(h02))
```

With the first guess $h(0)=1$, $g(\eta_\infty)\approx2.09$ rather than 1. The iteration converges to

$$f''(0)=h(0)\approx0.332,$$

the classic Blasius wall-shear value, and $g(\eta_\infty)=0.9999999\ldots$. The converged profile $u/U_\infty=f'(\eta)=g(\eta)$ rises smoothly from 0 at the wall to 1 by $\eta\approx5$.
