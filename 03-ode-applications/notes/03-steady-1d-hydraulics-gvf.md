---
title: Steady 1D River Hydraulics and Gradually Varied Flow
---

# Steady 1D River Hydraulics and Gradually Varied Flow

:::{admonition} Learning objectives
:class: tip
After this lesson you should be able to:

- reduce the Saint-Venant equations to the gradually varied flow ODE for steady flow
- write $dh/dx=(S_o-S_f)/(1-Fr^2)$ and explain each term
- relate the direct step method to an Euler step and the standard step method to an implicit one
:::

## From Saint-Venant to an ODE

The 1D governing equations are continuity and momentum:

$$\frac{\partial A}{\partial t}+\frac{\partial Q}{\partial x}=0,$$

$$\frac{\partial Q}{\partial t}+\frac{\partial}{\partial x}\left(\beta\frac{Q^2}{A}\right)+\frac{\partial}{\partial x}\left(gh_cA\right)=gA\,(S_o-S_f).$$

Assume steady flow, $\partial/\partial t=0$. The PDEs become ODEs:

- Continuity: $dQ/dx=0$, so $Q$ is constant.
- Momentum: $\dfrac{d}{dx}\left(\beta\dfrac{Q^2}{A}+gh_cA\right)=gA\,(S_o-S_f)$, with a velocity-head and a pressure-head term.

It can be shown that this reduces to

$$\frac{d}{dx}\left(\frac{V^2}{2g}+h\right)=S_o-S_f,\quad\text{or}\quad\frac{dE}{dx}=S_o-S_f,\qquad E=\frac{u^2}{2g}+h\ \text{(specific energy)}.$$

$S_f$ is the friction slope, the rate of energy lost to friction. It can be written $S_f=C_fFr^2$, where $C_f$ is a friction coefficient (related to the velocity and bed shear stress $\tau_B$) and $Fr=u/\sqrt{gh}$ is the Froude number.

Since $\dfrac{dE}{dx}=\dfrac{dE}{dh}\dfrac{dh}{dx}$ and $\dfrac{dE}{dh}=1-Fr^2$, the momentum equation can also be written

$$\frac{dh}{dx}=\frac{S_o-S_f}{1-Fr^2}=\frac{S_o-C_fFr^2}{1-Fr^2},$$

an ODE of the form $dh/dx=f[h(x)]$. This is the gradually varied flow (GVF) equation, the basis of steady HEC-RAS.

## The direct step method

In open-channel flow courses we teach the "direct step" method:

$$\frac{E_2-E_1}{x_2-x_1}=S_o-\bar S_f\quad\text{or}\quad E_{i+1}=E_i+\Delta x\,(S_o-\bar S_f).$$

This is an Euler step (of the energy equation). It is used by solving for the distance for a chosen change in energy,

$$\Delta x=\frac{E_{i+1}-E_i}{S_o-\bar S_f},\qquad\bar S_f=\tfrac12\left(S_{f,i}+S_{f,i+1}\right).$$

The friction slope comes from Manning's equation,

$$Q=\frac{c_0}{n}AR^{2/3}S_f^{1/2}\;\Rightarrow\;S_{f,i}=\left[\frac{Qn}{c_0A_iR_i^{2/3}}\right]^2,$$

with $c_0=1$ in SI units (1.49 in US customary units), or equivalently from $S_{f,i}=C_{f,i}Fr_i^2$. A resistance law such as the Strickler form $C_f^{-1/2}=U/u_*=\alpha\,(h/k_s)^{1/6}$, i.e. $C_f=\alpha^{-2}(h/k_s)^{-1/3}$, can be used for $C_f$.

There is nothing special about the direct step: it is just a numerical method.

## The standard step method

The standard step method takes the unknown to be $h_{i+1}$:

$$E_{i+1}=E_i+\Delta x\,(S_o-\bar S_f).$$

The only difference is that it is *implicit*: $\bar S_f$ needs $h_{i+1}$, so an iteration is required.

More generally, write $\dfrac{dh}{dx}=\dfrac{S_o-S_f}{1-Fr^2}$ and note that it is explicit if $S_f$ and $Fr$ are evaluated at $i$, and implicit if they also depend on $i+1$. For the homework, use the explicit form (RK4) of the $dh/dx$ equation.

## Check your understanding

**1.** What does steady flow do to the continuity and momentum equations?

:::{dropdown} Answer
Continuity becomes $dQ/dx=0$, so $Q$ is constant, and momentum becomes an ODE in $x$: $dE/dx=S_o-S_f$, which can be written $dh/dx=(S_o-S_f)/(1-Fr^2)$.
:::

**2.** What is $dE/dh$ for specific energy $E=u^2/2g+h$?

:::{dropdown} Answer
$dE/dh=1-Fr^2$.
:::

**3.** How does the direct step method relate to Euler's method?

:::{dropdown} Answer
It is an Euler step applied to the energy equation, $E_{i+1}=E_i+\Delta x(S_o-\bar S_f)$, solved for the distance $\Delta x$ given a chosen change in $E$.
:::

**4.** Why is the standard step method implicit?

:::{dropdown} Answer
It takes $h_{i+1}$ as the unknown, but $\bar S_f$ depends on $h_{i+1}$, so an iteration is needed at each step.
:::

**5.** What happens to the GVF equation as $Fr\to1$?

:::{dropdown} Answer
The denominator $1-Fr^2\to0$, so $dh/dx$ becomes singular. The equation cannot be integrated through critical flow.
:::
