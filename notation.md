---
title: Notation
---

# Notation

Symbols follow the lessons, which draw on several textbooks and papers, so a few letters do double duty. This page lists the conventions and the clashes to watch for. When in doubt, the lesson defines its symbols where they first appear.

## Grids and numerical methods

| Symbol | Meaning |
|---|---|
| $x, y, z, t$ | space coordinates and time |
| $\Delta x,\ \Delta t$ | grid spacing and time step |
| $i, j$ (subscript) | grid point index in space |
| $n$ or $k$ (superscript) | time level |
| $N$ | number of intervals (so $N+1$ grid points) |
| $\nu=c\ \Delta t/\Delta x$ | Courant number (advection) |
| $r=\nu_d\ \Delta t/\Delta x^2$ | diffusion number |
| $Pe_\Delta=\lvert c\rvert\Delta x/\nu_d$ | cell Péclet number |
| $G$ | amplification factor in von Neumann analysis |
| $\theta$ | wavenumber times $\Delta x$ (phase angle per grid point) |
| $K_0,\dots,K_3$ or $K_1,\dots,K_4$ | slope evaluations in a Runge–Kutta step |
| $\lambda$ | decay rate in the model problem $y'=-\lambda y$ |

## Fluid mechanics and hydraulics

| Symbol | Meaning |
|---|---|
| $u, v, w$ | velocity components |
| $\bar u$, $\tilde u$, $U$ or $V$ | time-averaged, depth-averaged and cross-section-averaged velocity |
| $u', \overline{u_i'u_j'}$ | velocity fluctuation and Reynolds stress |
| $p,\ \rho,\ \mu,\ \nu$ | pressure, density, dynamic viscosity, kinematic viscosity |
| $h$ | flow depth |
| $A,\ P,\ R,\ T$ | flow area, wetted perimeter, hydraulic radius, top width |
| $Q,\ q$ | discharge and discharge per unit width |
| $c=\sqrt{gh}$ | shallow-water wave speed |
| $Fr=\lvert u\rvert/c$ | Froude number |
| $S_o,\ S_f$ | bed slope and friction slope |
| $n,\ C_f$ | Manning's roughness and friction coefficient |
| $E=u^2/2g+h$ | specific energy |
| $\tau_B$ | bed shear stress |
| $\eta$ | bed elevation (modules 03 and 06) |

## Density-driven flows

| Symbol | Meaning |
|---|---|
| $\rho_a,\ \Delta\rho=\rho_a-\rho$ | ambient density and density deficit of a plume |
| $g'=\dfrac{\rho-\rho_a}{\rho}\ g$ | reduced gravity (magnitude used in the plume equations) |
| $Fr_d=u/\sqrt{g'h}$ | densimetric Froude number |
| $Ri=g'h/u^2=1/Fr_d^2$ | bulk Richardson number |
| $w_e,\ \delta=w_e/u$ | entrainment velocity and entrainment ratio |
| $w$ | plume width |

## Sediment

| Symbol | Meaning |
|---|---|
| $C$ | concentration of a dissolved or suspended substance |
| $q_t,\ q_s,\ q_b$ | total, suspended and bed-load sediment flux per unit width |
| $\lambda_p$ | bed porosity |
| $\tau^*=\tau_B/(\rho g R_s d)$ | dimensionless bed shear stress (Shields stress) |
| $R_s=(\rho_s-\rho)/\rho$ | submerged specific gravity of the sediment |
| $d$ | grain diameter |

## Letters that mean more than one thing

| Letter | Meanings (and where) |
|---|---|
| $\nu$ | Kinematic viscosity (Navier–Stokes, module 01); Courant number $c\Delta t/\Delta x$ (modules 05, 06). The diffusion coefficient is written $\nu_d$ in the stability and scheme lessons, but plain $\nu$ in the model-equation lesson. |
| $\lambda$ | Decay rate (Euler stability, module 02); scaling factor (Blasius shortcut, module 04); bed porosity is $\lambda_p$ (module 06). |
| $g$ | Gravitational acceleration; the slope function $g(\xi,t)$ in some ODE notes; $g=f'$ in the Blasius problem. |
| $G$ | Pressure gradient $dp/dx$ (Poiseuille–Couette, module 04); amplification factor (von Neumann analysis, module 05). |
| $h$ | Flow depth; step size in some numerical-methods texts; $h=f''$ in the Blasius system. |
| $f$ | Right-hand side function of an ODE; the Blasius stream function. |
| $z_b$, $\eta$ | Bed elevation: $z_b$ in module 01, $\eta$ in modules 03 and 06. |
| $u$ | Velocity; also the generic unknown in the model PDEs of module 05. |
| $C$ | Concentration (modules 03 and 05); $C_f$ is a friction coefficient. |
