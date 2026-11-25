---
title: 1D Unsteady Hydraulics - Boundary Conditions and Implicit Schemes
---

# Boundary Conditions and Implicit Schemes

## Boundary conditions

At the ends of a reach, the Saint-Venant equations need boundary information. For subcritical flow ($Fr<1$), one condition is needed at each end; for supercritical flow, both are specified upstream.

**Method of characteristics (specified intervals).** Along the characteristics $C1$ and $C2$ (with wave speed $c=\sqrt{gD}$), the equations reduce to ordinary differential relations. For a point $P$ at the new time level, with feet $R$ and $S$ on the old level:

$$\begin{aligned}C1&:\;V_P+\frac{gy_P}{c_R}=V_R+\frac{gy_R}{c_R}+g(S_o-S_{fR})\Delta t=K_R,&x_P-x_R&=(V_R+c_R)\Delta t\\C2&:\;V_P-\frac{gy_P}{c_S}=V_S-\frac{gy_S}{c_S}+g(S_o-S_{fS})\Delta t=K_S,&x_P-x_S&=(V_S-c_S)\Delta t\end{aligned}$$

At the upstream boundary only the C2 relation reaches the boundary, and at the downstream boundary only C1. Combine the one relation with a specified value, $y(t)$ or $V(t)$ (or a relation among them below). In practice one often uses a combination of specified values and the method of characteristics.

**Other options**

| Condition | Relation |
|---|---|
| Upstream reservoir | $y_i^{k+1}=y_{res}+(1+K)\dfrac{(V_{i,1}^{k+1})^2}{2g}$ |
| Downstream reservoir | $y_{i,n+1}^{k+1}=y_{res}-(1-K)\dfrac{(V_{i,n+1}^{k+1})^2}{2g}$ |
| Sluice gate | $Q_{i,n+1}^{k+1}=C_dA_g\sqrt{2g\,y_{i,n+1}^{k+1}}$ |
| Rating curve | $Q=f(y_{i,n+1}^{k+1})$ |
| Series junction | continuity $V_{i,n+1}A_{i,n+1}=V_{i+1,1}A_{i+1,1}$ and energy $z_i+y_{i,n+1}+\dfrac{V_{i,n+1}^2}{2g}=z_{i+1}+y_{i+1,1}+(1+K)\dfrac{V_{i+1,1}^2}{2g}$ |

## Implicit schemes

Explicit schemes are limited by a stability (Courant) condition on the time step. **Implicit** schemes evaluate the spatial derivatives at the new time level $k+1$ (e.g. backward, $\partial f/\partial x=(f_i^{k+1}-f_{i-1}^{k+1})/\Delta x$), so all points at the new level are coupled and must be solved together. In return they offer increased stability and larger time steps.

### Preissmann scheme

A four-point ("box") scheme with weighting factor $\alpha$:

$$\frac{\partial f}{\partial t}=\frac{(f_i^{k+1}+f_{i+1}^{k+1})-(f_i^k+f_{i+1}^k)}{2\Delta t},\quad\frac{\partial f}{\partial x}=\frac{\alpha(f_{i+1}^{k+1}-f_i^{k+1})+(1-\alpha)(f_{i+1}^k-f_i^k)}{\Delta x},$$

and $f=\tfrac12\alpha(f_i^{k+1}+f_{i+1}^{k+1})+\tfrac12(1-\alpha)(f_i^k+f_{i+1}^k)$ for variables like $S_f$. The conservative system becomes

$$\mathbf U_i^{k+1}+\mathbf U_{i+1}^{k+1}+2\frac{\Delta t}{\Delta x}\left[\alpha(\mathbf F_{i+1}^{k+1}-\mathbf F_i^{k+1})+(1-\alpha)(\mathbf F_{i+1}^k-\mathbf F_i^k)\right]+\Delta t\left[\alpha(\mathbf S_i^{k+1}+\mathbf S_{i+1}^{k+1})+(1-\alpha)(\mathbf S_{i+1}^k+\mathbf S_i^k)\right]=\mathbf U_i^k+\mathbf U_{i+1}^k.$$

- $\alpha=0$: fully explicit; $\alpha=1$: fully implicit.
- Stable for $0.55<\alpha\le1$. Smaller $\alpha$ gives a sharper wave front but less damping of oscillations.

**Counting equations.** Each segment between nodes $i$ and $i+1$ gives 2 equations (mass and momentum). With $N$ segments there are $2N$ equations and $2(N+1)$ unknowns ($y$ and $V$ at each of $N+1$ nodes). The 2 remaining equations are the **2 boundary conditions**.

### Implicit solution procedure

1. Write the system of equations at each node (segment).
2. Add the boundary conditions.
3. Solve the resulting system of **nonlinear** equations, e.g. by Newton–Raphson:
   - Estimate the unknowns $A$ and $V$.
   - With the Jacobian $J_{ij}=\partial F_i/\partial x_j$, linearize $\vec F(\vec x+\delta\vec x)=\vec F(\vec x)+J\,\delta\vec x+O(\delta\vec x^2)$.
   - Solve $J\,\delta\vec x=-\vec F$ for $\delta\vec x$ (the linear solve from the [relaxation note](../../04-boundary-value-problems/notes/01-relaxation-method.md)) and update $\vec x_{new}=\vec x_{old}+\delta\vec x$.
   - Repeat until $\delta\vec x$ is small (this needs the partial derivatives of the equations and boundary conditions).
