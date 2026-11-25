# Introduction: Why Model Environmental Flows?

*Transcribed from the Lecture 1 handout and instructor notes.*

## Complex fluid environments are everywhere

Rivers, estuaries, deltas, river plumes and turbulent jets all involve flow, transport and change at the bed. Predicting how they behave is the purpose of this course.

## Quantities of interest

**Water**

1. **Depth**: what is the flood level?
2. **Velocity**: can a fish swim through this section of river?
3. **Stress**: will sediment erode or deposit at this location?

**Other substances**

1. **Bed elevation and grain size**: how is the system responding to hydrology and sea level?
2. **Suspended sediment concentration**: loading to a reservoir or bay, water clarity.
3. **Dissolved oxygen (DO)**: what is the available oxygen level in the bay?
4. **Nutrients**.
5. **Salt**: where is the salt front in a coastal river?

## The central question

> How do we predict the movement of water and of substances in the water, and the changes that can take place within the water column and at the bed?

## Model the system mathematically

Governing equations are based on three principles:

1. **Conservation of mass**
   - Continuity equation (water mass or volume)
   - Advection-diffusion equation (conservation of a substance in the flow)
   - Exner equation (conservation of sediment mass in the bed and banks)
2. **Conservation of momentum**
   - Navier-Stokes equations (and all their variants)
3. **Conservation of energy**
   - Energy equation

Solving the system of equations gives the quantities of interest.

### Example

Navier-Stokes (momentum), in index notation:

$$
\frac{Du_i}{Dt} = \frac{\partial u_i}{\partial t} + u_j\frac{\partial u_i}{\partial x_j}
= g_i - \frac{1}{\rho}\frac{\partial p}{\partial x_i} + \nu\frac{\partial^2 u_i}{\partial x_j^2}
$$

Continuity:

$$
\frac{\partial u_i}{\partial x_i} = 0
$$

Advection-diffusion of a scalar $C$:

$$
\frac{\partial C}{\partial t} + u_i\frac{\partial C}{\partial x_i}
= \frac{\partial}{\partial x_i}\left[\left(D_m + D_{T,i}\right)\frac{\partial C}{\partial x_i}\right] + r_g - r_d
$$

where $D_m$ is molecular diffusivity, $D_{T,i}$ is turbulent diffusivity, and $r_g$ and $r_d$ are growth and decay (source and sink) terms.

### Does the system close?

The solution gives

$$
u_i = u_i(x,y,z,t), \qquad p = p(x,y,z,t), \qquad C = C(x,y,z,t)
$$

That is **5 unknowns** ($u$, $v$, $w$, $p$, $C$) and **5 equations** (3 momentum, 1 continuity, 1 advection-diffusion). The count works out, so this should be okay... right?

## The problem

Analytic solutions exist only for simplified conditions (for example, laminar flow between parallel plates with a velocity profile $u = u(y)$). Natural flows are complex: braided channels, turbulent and sediment-laden flow, irregular geometry.

## The numerical approach

Numerical methods solve the governing equations for complex environments:

1. **Continuous** physical domain and governing PDEs
2. becomes a **discrete** physical domain and a system of algebraic equations
3. which is **solved on a computer**.

## Course outline

- **Part I: Introductory topics**: ideas, terms and equations.
- **Part II: Building understanding and skill with simplified systems**: finite difference (FD) introduction, ODEs, PDEs.
- **Part III: Modeling more complex settings**: 1D (Saint-Venant and HEC-RAS), 2D (HEC-RAS), 3D (Delft3D).

## Tools

**Programming.** Will you need to program? Yes. Which language? Python.

**Computational packages**

1. **HEC-RAS**
   - 1D Saint-Venant equations (dynamic wave routing)
   - 2D shallow water
2. **Delft3D**
   - 2D and 3D vertical hydrodynamics
   - Transport

### What is Python?

- A general-purpose programming language with a large scientific computing ecosystem (NumPy, pandas, SciPy, Matplotlib, and more).
- Common environments: CoCalc (online), IPython terminal, Spyder IDE (Matlab-like), Jupyter notebook, JupyterLab.
- If you have a problem to solve, you can most likely find a library to help, and it is probably on GitHub.

### What is HEC-RAS?

Designed to perform one- and two-dimensional hydraulic calculations for a full network of natural and constructed channels (US Army Corps of Engineers, Hydrologic Engineering Center).

- Areas of application: steady flow water surface profiles; one- and two-dimensional unsteady flow simulation; sediment transport and movable boundary computations; water quality analysis.
- Free, and the industry standard for flood analysis and hydraulic design.

### What is Delft3D?

A multi-dimensional (2D or 3D) hydrodynamic and transport simulation program that computes non-steady flow and transport from tidal and meteorological forcing on a rectilinear or curvilinear, boundary-fitted grid. In 3D simulations the vertical grid follows a $\sigma$ co-ordinate approach.

- Areas of application: tides and wind-driven flows; stratified and density-driven flows; river flows; deep lakes and reservoirs; tsunamis, hydraulic jumps and flood waves; freshwater discharge into bays; saltwater intrusion; thermal stratification; cooling water intakes and waste water outlets; transport of dissolved material; sediment transport and morphological change.
- Open source, free, and a standard in coastal sediment transport and research applications.

## Why this course?

Instructor talking points:

- Numerical analysis is excellent for building insight, including into modern theory. *(Add examples.)*
- Numerical simulations are less expensive than physical models, so they get used. *(Add examples.)*
- Models are the primary tool of consulting.
- Most numerical-methods coursework is geared toward mechanical and aerospace applications, not environmental flows.
