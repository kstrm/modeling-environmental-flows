---
title: Initial Value ODEs in Natural and Engineered Systems
---

# Initial Value ODEs in Natural and Engineered Systems

What kinds of problems present themselves as an initial value ODE or a set of ODEs? The system must:

1. depend on only one variable (a general $x$, or time), and
2. have no constraint on the far field.

The basic equations are conservation of mass (continuity, advection–diffusion),

$$\frac{dM}{dt}=\sum\dot m_{in}-\sum\dot m_{out},$$

and conservation of momentum, $\sum F=ma$. In general these depend on $x,y,z,t$. The only way to end up with an ODE is to **simplify the system**. How? (Ask: what ideas do you have?)

## Remove all spatial change

- **Well-mixed tanks:** mass or volume conservation depends on time only.
- **Level-pool routing** of a lake or reservoir: assume the same (a level water surface, so storage depends only on time).
- **Uniform (well-mixed) channel or flume** with no spatial gradients: in the advection–diffusion equation for depth-averaged concentration,

  $$\frac{\partial(ch)}{\partial t}+\frac{\partial(cuh)}{\partial x}=\frac{\partial}{\partial x}\left(D\frac{\partial c}{\partial x}\right)+E-D_p,$$

  setting $\partial/\partial x=0$ leaves $\dfrac{d(ch)}{dt}=E-D_p$ (erosion minus deposition).

## Remove two spatial directions and time (steady 1D problems)

- Simplified Saint-Venant equations, steady and 1D, give **gradually varied flow (GVF)** (the basis of steady HEC-RAS): water-surface profiles that rise or fall along the channel.
- Simplified 1D **jets, plumes and density currents** at steady state:
  - a *jet* is driven by momentum,
  - a *plume* is driven by a density difference (buoyancy),
  - a *density current* is a gravity-driven bottom (or surface) current.

We will spend time with all of these in lecture or homework, starting with the mixing-tank problem.

## Example: three tanks in series

Three well-mixed tanks of volumes $V_1=20$ L, $V_2=40$ L and $V_3=60$ L are connected in series; $Q_{in}=Q=Q_{out}=10$ L/min. The initial concentration is $35$ ppt in every tank and the incoming concentration is $C_{in}=0$ (flushing with fresh water). What do the concentration time series $C_1(t)$, $C_2(t)$, $C_3(t)$ look like?

A mass balance for each tank gives

$$
\begin{aligned}
\frac{d(C_1V_1)}{dt}&=C_{in}Q-C_1Q&\Rightarrow\;&\frac{dC_1}{dt}=\frac{C_{in}}{V_1}Q-\frac{C_1}{V_1}Q\\
\frac{d(C_2V_2)}{dt}&=C_1Q-C_2Q&\Rightarrow\;&\frac{dC_2}{dt}=\frac{C_1}{V_2}Q-\frac{C_2}{V_2}Q\\
\frac{d(C_3V_3)}{dt}&=C_2Q-C_3Q&\Rightarrow\;&\frac{dC_3}{dt}=\frac{C_2}{V_3}Q-\frac{C_3}{V_3}Q
\end{aligned}
$$

**Handout version.** The classroom handout gives the system with a deliberate error, to be used as a lesson:

$$\frac{dC_1}{dt}=-\tfrac12C_1,\qquad\frac{dC_2}{dt}=\tfrac12C_1-\tfrac14C_2,\qquad\frac{dC_3}{dt}=\tfrac14C_2-\tfrac16C_3.$$

The loss terms are right ($Q/V_i=\tfrac12,\tfrac14,\tfrac16$ per minute), but the inflow terms use the *upstream* tank's volume ($Q/V_1$ and $Q/V_2$) instead of the receiving tank's volume. The correct system is

$$\frac{dC_1}{dt}=-\tfrac12C_1,\qquad\frac{dC_2}{dt}=\tfrac14C_1-\tfrac14C_2,\qquad\frac{dC_3}{dt}=\tfrac16C_2-\tfrac16C_3.$$

The point of the exercise: a numerical solution of the wrong equations still runs and produces smooth curves, so you must critically examine the output (e.g., does total salt mass behave physically? do the curves make sense?).
