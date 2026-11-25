---
title: Glossary
---

# Glossary

Short definitions of terms used in the lessons, with a link to where each is developed.

**Advection.** Transport of a quantity by the flow. It translates a profile without changing its shape. [PDE model equations](05-pdes/notes/01-pdes-classification-and-model-equations.md)

**Amplification factor ($G$).** The factor by which one Fourier mode of the numerical solution is multiplied each time step. A scheme is stable only if $\lvert G\rvert\le1$. [Stability and von Neumann analysis](05-pdes/notes/03-stability-cfl-and-von-neumann.md)

**Backwater.** The raised water surface upstream of a downstream control (such as the sea or a dam), computed from the gradually varied flow equation. [Steady 1D hydraulics](03-ode-applications/notes/03-steady-1d-hydraulics-gvf.md)

**Boundary condition (BC).** A value or relation imposed at the edge of the domain. [Components of a model](01-governing-equations/notes/01-components-of-a-model-and-governing-equations.md)

**Boundary value problem (BVP).** An ODE with conditions given at both ends of the domain, solved all at once rather than marched. [Relaxation method](04-boundary-value-problems/notes/01-relaxation-method.md)

**Boussinesq approximation.** In density-driven flows, replacing $g$ by the reduced gravity $g'$ and otherwise treating density as constant. [Stratified flows](03-ode-applications/notes/04-stratified-flows-jets-and-plumes.md)

**Bore.** A moving, abrupt rise in water depth (a hydraulic shock), as at the front of a dam-break wave. [Saint-Venant equations](06-1d-unsteady-hydraulics/notes/00-saint-venant-equations-and-wave-speeds.md)

**Characteristics.** Curves in the $x$–$t$ plane along which information travels, at speeds $u\pm c$ for the Saint-Venant equations. [Saint-Venant equations](06-1d-unsteady-hydraulics/notes/00-saint-venant-equations-and-wave-speeds.md)

**Closure.** An extra relation that supplies a quantity the conservation laws leave unknown (for example the Reynolds stress, bed shear stress, exit velocity of a tank or sediment transport rate). [Components of a model](01-governing-equations/notes/01-components-of-a-model-and-governing-equations.md)

**Consistency.** A scheme is consistent if its truncation error goes to zero as $\Delta x,\Delta t\to0$. [Stability and von Neumann analysis](05-pdes/notes/03-stability-cfl-and-von-neumann.md)

**Conservation form.** Writing the equations as $\mathbf U_t+\mathbf F_x=\mathbf G$, with conserved variables $\mathbf U$, fluxes $\mathbf F$ and sources $\mathbf G$. [Explicit schemes](06-1d-unsteady-hydraulics/notes/01-governing-equations-and-explicit-schemes.md)

**Convergence.** The numerical solution approaches the true solution as the grid is refined. [Stability and von Neumann analysis](05-pdes/notes/03-stability-cfl-and-von-neumann.md)

**Courant number ($\nu$).** $c\,\Delta t/\Delta x$: the number of grid cells information travels per time step. [Stability and von Neumann analysis](05-pdes/notes/03-stability-cfl-and-von-neumann.md)

**CFL condition.** The requirement that the numerical domain of dependence include the physical one; for the schemes in this course, $\nu\le1$. [Stability and von Neumann analysis](05-pdes/notes/03-stability-cfl-and-von-neumann.md)

**Crank–Nicolson.** An implicit scheme that averages the spatial terms at the old and new time levels; the PDE counterpart of the trapezoidal rule. [Adams–Bashforth–Moulton](02-finite-differences-and-odes/notes/05-adams-bashforth-moulton.md)

**Diffusion.** Spreading caused by gradients; it lowers peaks and smooths profiles. [PDE model equations](05-pdes/notes/01-pdes-classification-and-model-equations.md)

**DNS, LES, RANS.** Direct numerical simulation (resolve all turbulence), large eddy simulation (resolve large eddies and model small ones) and Reynolds-averaged Navier–Stokes (average the turbulence out and model it). [Components of a model](01-governing-equations/notes/01-components-of-a-model-and-governing-equations.md)

**Domain of dependence.** The set of points whose values can influence the solution at a given point, physically or numerically. [Stability and von Neumann analysis](05-pdes/notes/03-stability-cfl-and-von-neumann.md)

**Entrainment.** Incorporation of ambient fluid into a jet or plume, which increases its volume and dilutes it. [River mouth plume](03-ode-applications/notes/05-river-mouth-plume.md)

**Exner equation.** Conservation of sediment in the bed: $(1-\lambda_p)\partial\eta/\partial t=-\partial q_t/\partial x$. [Exner equation](06-1d-unsteady-hydraulics/notes/03-morphodynamics-exner-equation.md)

**Explicit and implicit schemes.** Explicit schemes compute new values directly from old ones; implicit schemes couple the new values and require solving an equation or linear system. [Euler's method](02-finite-differences-and-odes/notes/01-eulers-method.md)

**Finite difference.** An approximation of a derivative by differences of function values at grid points. [Spatial discretization](02-finite-differences-and-odes/notes/06-spatial-discretization.md)

**Froude number ($Fr$).** The ratio of flow speed to wave speed, $\lvert u\rvert/\sqrt{gh}$. Flow is subcritical for $Fr<1$, supercritical for $Fr>1$ and transcritical when it passes through 1. [Saint-Venant equations](06-1d-unsteady-hydraulics/notes/00-saint-venant-equations-and-wave-speeds.md)

**Gradually varied flow (GVF).** Steady flow in which depth changes slowly along the channel, governed by $dh/dx=(S_o-S_f)/(1-Fr^2)$. [Steady 1D hydraulics](03-ode-applications/notes/03-steady-1d-hydraulics-gvf.md)

**Godunov's theorem.** No linear scheme of higher than first order can be monotone. [Upwind, Lax and implicit schemes](05-pdes/notes/04-upwind-lax-and-implicit-schemes.md)

**Initial value problem (IVP).** An ODE or PDE with conditions given at the start, marched forward in time (or space). [Initial value ODEs](03-ode-applications/notes/02-initial-value-odes-in-natural-systems.md)

**Modified equation.** The equation a scheme actually solves, found from the truncation error; it reveals numerical diffusion. [Stability and von Neumann analysis](05-pdes/notes/03-stability-cfl-and-von-neumann.md)

**Monotone.** A scheme that creates no new maxima or minima, so it does not produce wiggles. [Upwind, Lax and implicit schemes](05-pdes/notes/04-upwind-lax-and-implicit-schemes.md)

**Numerical diffusion.** Smearing introduced by the truncation error of a scheme (for FTBS, a diffusion coefficient $\tfrac{c\Delta x}{2}(1-\nu)$). [Stability and von Neumann analysis](05-pdes/notes/03-stability-cfl-and-von-neumann.md)

**Order of accuracy.** The power of the step size with which the error shrinks. Euler is first order and RK4 is fourth order. [Euler error, Taylor series and stability](02-finite-differences-and-odes/notes/02-accuracy-taylor-series-and-stability.md)

**Plume.** A flow driven by a density difference, such as fresh river water spreading over salty ambient water. [Stratified flows](03-ode-applications/notes/04-stratified-flows-jets-and-plumes.md)

**Reduced gravity ($g'$).** Gravity scaled by the relative density difference, $g'=(\rho-\rho_a)g/\rho$. [Stratified flows](03-ode-applications/notes/04-stratified-flows-jets-and-plumes.md)

**Reynolds stress.** The averaged product of velocity fluctuations, $\overline{u_i'u_j'}$, which appears when the Navier–Stokes equations are time averaged. [Components of a model](01-governing-equations/notes/01-components-of-a-model-and-governing-equations.md)

**Richardson number ($Ri$).** The ratio of buoyancy to inertia, $g'h/u^2$. [Stratified flows](03-ode-applications/notes/04-stratified-flows-jets-and-plumes.md)

**Runge–Kutta methods.** Single-step schemes that use several slope evaluations within a step; RK4 is the classical fourth-order method. [Runge–Kutta methods](02-finite-differences-and-odes/notes/03-runge-kutta-methods.md)

**Saint-Venant equations.** The 1D, cross-section-averaged equations of mass and momentum for unsteady open-channel flow. [Saint-Venant equations](06-1d-unsteady-hydraulics/notes/00-saint-venant-equations-and-wave-speeds.md)

**Shock capturing.** Numerical schemes that compute discontinuities such as bores without tracking them explicitly. [Explicit schemes](06-1d-unsteady-hydraulics/notes/01-governing-equations-and-explicit-schemes.md)

**Stability.** A scheme is stable if errors do not grow as the calculation marches forward. [Euler error, Taylor series and stability](02-finite-differences-and-odes/notes/02-accuracy-taylor-series-and-stability.md)

**Stencil.** The set of grid points used to compute one new value or derivative. [Spatial discretization](02-finite-differences-and-odes/notes/06-spatial-discretization.md)

**Truncation error.** The error made by cutting off the Taylor series in a difference approximation. [Euler error, Taylor series and stability](02-finite-differences-and-odes/notes/02-accuracy-taylor-series-and-stability.md)

**TVD (total variation diminishing).** A property of schemes (or a dissipation step) that prevents new oscillations from appearing. [Explicit schemes](06-1d-unsteady-hydraulics/notes/01-governing-equations-and-explicit-schemes.md)

**Upwinding.** Taking spatial differences from the side the flow comes from. [Upwind, Lax and implicit schemes](05-pdes/notes/04-upwind-lax-and-implicit-schemes.md)

**Vectorization.** Replacing a loop over grid points by a single array operation using slicing. [Advection equation](05-pdes/notes/02-advection-equation-ftbs-ftcs.md)

**von Neumann analysis.** A stability test that follows a Fourier mode through the scheme and checks $\lvert G\rvert\le1$. [Stability and von Neumann analysis](05-pdes/notes/03-stability-cfl-and-von-neumann.md)
