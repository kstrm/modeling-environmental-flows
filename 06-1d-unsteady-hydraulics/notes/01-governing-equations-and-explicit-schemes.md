---
title: 1D Unsteady Hydraulics - Governing Equations and Explicit Schemes
---

# 1D Unsteady Hydraulics: Governing Equations and Explicit Schemes

A brief introduction to the Saint-Venant equations and a few discretization methods. See Chaudhry (2008), *Open-Channel Flow*, for more.

## Governing equations

With flow area $A$, discharge $Q$, depth $y$, velocity $V$, hydraulic depth $D$, top width $B$, lateral inflow per unit length $q_l$, bed slope $S_o$ and friction slope $S_f$:

**Conservation of mass**

$$\frac{\partial A}{\partial t}+\frac{\partial Q}{\partial x}=q_l\quad\Longleftrightarrow\quad\frac{\partial y}{\partial t}+D\frac{\partial V}{\partial x}+V\frac{\partial y}{\partial x}-\frac{q_l}{B}=0$$

**Conservation of momentum**

$$\frac{\partial Q}{\partial t}+\frac{\partial(QV)}{\partial x}+gA\frac{\partial y}{\partial x}=V_xq_l+gA(S_o-S_f)\quad\Longleftrightarrow\quad\frac{\partial V}{\partial t}+g\frac{\partial}{\partial x}\left(\frac{V^2}{2g}+y\right)=g(S_o-S_f)$$

### Vector forms

Non-conservative form, $\partial\mathbf U/\partial t+\mathbf A\,\partial\mathbf U/\partial x=\mathbf S$ with

$$\mathbf U=\begin{pmatrix}y\\V\end{pmatrix},\quad\mathbf A=\begin{pmatrix}V&D\\g&V\end{pmatrix},\quad\mathbf S=\begin{pmatrix}-q_l/B\\g(S_o-S_f)\end{pmatrix}.$$

Conservative form, $\mathbf U_t+\mathbf F_x+\mathbf S=\mathbf 0$ with

$$\mathbf U=\begin{pmatrix}A\\VA\end{pmatrix},\quad\mathbf F=\begin{pmatrix}VA\\V^2A+gA\bar y\end{pmatrix},\quad\mathbf S=\begin{pmatrix}0\\-gA(S_o-S_f)\end{pmatrix},$$

where $\bar y$ is the depth of the centroid of the cross section.

## Discretization

A grid of points $(i,k)$ with $i=0,\ldots,N-1$ in space and $k=0,\ldots,M-1$ in time. Spatial derivatives of $f_i^k$ in **explicit** schemes use only time level $k$:

| Difference | $\partial f/\partial x$ |
|---|---|
| Backward | $(f_i^k-f_{i-1}^k)/\Delta x$ |
| Forward | $(f_{i+1}^k-f_i^k)/\Delta x$ |
| Central | $(f_{i+1}^k-f_{i-1}^k)/2\Delta x$ |

## Explicit schemes

### Lax method

Replace $f_i^k$ in the time derivative by the average of its neighbors, $f^*=\tfrac12(f_{i-1}^k+f_{i+1}^k)$, and use central differences in space:

$$\mathbf U_i^{k+1}=\tfrac12\left(\mathbf U_{i+1}^k+\mathbf U_{i-1}^k\right)-\frac12\frac{\Delta t}{\Delta x}\left(\mathbf F_{i+1}^k-\mathbf F_{i-1}^k\right)-\mathbf S^*\Delta t,\qquad S_f^*=\tfrac12\left(S_{f,i-1}^k+S_{f,i+1}^k\right).$$

For the $(y,V)$ form this gives

$$\begin{aligned}y_i^{k+1}&=\tfrac12(y_{i-1}^k+y_{i+1}^k)-\frac12\frac{\Delta t}{\Delta x}D_i^*(V_{i+1}^k-V_{i-1}^k)-\frac12\frac{\Delta t}{\Delta x}V_i^*(y_{i+1}^k-y_{i-1}^k),\\V_i^{k+1}&=\tfrac12(V_{i+1}^k+V_{i-1}^k)-\frac12\frac{\Delta t}{\Delta x}g(y_{i+1}^k-y_{i-1}^k)-\frac12\frac{\Delta t}{\Delta x}V_i^*(V_{i+1}^k-V_{i-1}^k)+g\Delta t(S_o-S_f^*).\end{aligned}$$

Compare with the FTCS scheme from the [advection note](../../05-pdes/notes/02-advection-equation-ftbs-ftcs.md): averaging the neighbors stabilizes it, at the cost of added numerical diffusion.

### MacCormack scheme (explicit, shock capturing)

A predictor–corrector method that uses a backward difference in the predictor and a forward difference in the corrector.

- **Predictor:** $\mathbf U_i^*=\mathbf U_i^k-\dfrac{\Delta t}{\Delta x}\left(\mathbf F_i^k-\mathbf F_{i-1}^k\right)-\mathbf S_i^k\Delta t$
- **Corrector:** $\mathbf U_i^{**}=\mathbf U_i^k-\dfrac{\Delta t}{\Delta x}\left(\mathbf F_{i+1}^*-\mathbf F_i^*\right)-\mathbf S_i^*\Delta t$
- **Update:** $\mathbf U_i^{k+1}=\tfrac12\left(\mathbf U_i^*+\mathbf U_i^{**}\right)$

The result is second-order accurate in space and time and captures shocks, which matters in fluvial hydraulics where flow can pass through critical depth.

## Example: a shock-capturing scheme for a steep, flashy stream

**Motivation.** Steep, ephemeral, flash-flood-prone streams (e.g. the Texas Hill Country, with steep slopes and mixed bedrock–alluvial beds) can switch rapidly between subcritical and supercritical flow (*transcritical* flow), and a roadway crossing of such a stream can be overtopped within minutes. Modeling the flow and the bed change together requires a scheme that handles transcritical flow.

**Conditions to model.** Flow depth $h(x,t)$, bed elevation $\eta(x,t)$, unit discharge $q$ and unit bed-load flux $q_s$, with a channel width $w(x)$ that varies in plan through a culvert or contraction.

**Governing equations.**

$$\begin{aligned}\frac{\partial A}{\partial t}+\frac{\partial Q}{\partial x}&=0&&\text{(water volume)}\\\frac{\partial Q}{\partial t}+\frac{\partial}{\partial x}\left(\frac{Q^2}{A}+\frac{gh^2w}{2}\right)&=\frac{gh^2}{2}\frac{\partial w}{\partial x}+gA(S_0-S_f)&&\text{(momentum)}\\\frac{\partial\eta}{\partial t}+\frac{\partial}{\partial x}\left(\frac{q_s}{1-\lambda_p}\right)&=\frac{-1}{w}\frac{\partial w}{\partial x}\left(\frac{q_s}{1-\lambda_p}\right)&&\text{(sediment bed volume)}\end{aligned}$$

with $\lambda_p$ the bed porosity. **Closure** is given by the width function $w(x)$, Manning's equation for $S_f$, and a bed-load equation for $q_s$.

**Method.** A classic finite-difference MacCormack scheme, with a TVD (total variation diminishing) step and an improved source-term treatment, applied to

$$\frac{\partial\mathbf U}{\partial t}+\frac{\partial\mathbf F}{\partial x}=\mathbf G,\quad\mathbf U=\begin{bmatrix}A\\Q\\\eta\end{bmatrix},\;\mathbf F=\begin{bmatrix}Q\\Q^2/A+gh^2w/2\\q_s/(1-\lambda_p)\end{bmatrix},\;\mathbf G=\begin{bmatrix}0\\\frac{gh^2}{2}\frac{\partial w}{\partial x}+gA(S_0-S_f)\\-\frac1w\frac{\partial w}{\partial x}\frac{q_s}{1-\lambda_p}\end{bmatrix}.$$

$$\mathbf U_i^*=\mathbf U_i^k-\frac{\Delta t}{\Delta x}(\mathbf F_{i+1}^k-\mathbf F_i^k)+\Delta t\,\mathbf G_i^k,\quad\mathbf U_i^{**}=\mathbf U_i-\frac{\Delta t}{\Delta x}(\mathbf F_i^*-\mathbf F_{i-1}^*)+\Delta t\,\mathbf G_i^*,\quad\mathbf U_i^{k+1}=0.5(\mathbf U_i^*+\mathbf U_i^{**})+\lambda\left(\mathbf D_{i+\frac12}^k-\mathbf D_{i-\frac12}^k\right),$$

where the last term is the TVD dissipation. Treating the source terms so that they balance the flux gradients (Tseng, 2003) removes the spurious discharge oscillations that otherwise appear over a sloping, uneven bed.

**Testing.** The model is checked against cases with known behavior: slope changes (with transitions between sub- and supercritical flow), dam break, and vertical and lateral contractions for the hydrodynamics, then sediment expansion and contraction cases for bed change (bed load computed from a power-law or a Meyer-Peter–Müller type relation).

## Further reading

- Chaudhry (2008), *Open-Channel Flow*, for the schemes above.
- Bhallamudi and Chaudhry (1991) and Papanicolaou et al. (2004, 2010) for the MacCormack-with-TVD approach to coupled flow and bed change.
