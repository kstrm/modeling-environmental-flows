---
title: Modeling of Environmental Flows
---

# Modeling of Environmental Flows

How do we predict the movement of water and of the substances it carries (sediment, salt, nutrients, contaminants), and the changes that take place in the water column and at the bed? This course introduces the numerical methods used to answer that question in rivers, estuaries and other natural environments, and gives you hands-on practice coding simple flow and transport problems yourself.

The first half builds understanding and skill with simplified systems: finite-difference theory applied to ODEs and PDEs, with an emphasis on writing your own solvers in Python. The second half moves to more complex settings: 1D unsteady hydraulics (Saint-Venant equations), 2D shallow water modeling, and 3D modeling with freely available tools such as HEC-RAS and Delft3D.

## Who this is for

Graduate and advanced undergraduate students in civil and environmental engineering, geoscience and related fields. You should be comfortable with the differential forms of the equations of motion and transport. No prior programming experience is assumed; the first module gets you started with Python and Jupyter.

## How the course is organized

Each module contains lesson notes, notebooks to work through, and exercises.

| Module | Topics |
|---|---|
| 00 Getting started | Python, Jupyter notebooks, first steps with arrays and plots |
| 01 Governing equations | Conservation laws, averaging, laminar vs turbulent flow, model resolution |
| 02 Finite differences and ODEs | Euler method, accuracy, stability, Runge-Kutta, ODE systems |
| 03 ODE applications | Mixing tanks, gradually varied flow, stratified flow and river plumes |
| 04 Boundary value problems | Linear systems, Couette-Poiseuille flow, Blasius boundary layer |
| 05 PDEs | Advection, diffusion, advection-diffusion, CFL stability, bed morphodynamics |
| 06 1D unsteady hydraulics | Saint-Venant equations, the bridge to HEC-RAS |

Modules on HEC-RAS (1D and 2D) and Delft3D (3D) will follow.

## Using the notebooks

Every lecture notebook comes in two versions. The **student version** has blanks for you to fill in and lives in each module's `notebooks/` folder in the [GitHub repository](https://github.com/kstrm/modeling-environmental-flows). The **completed version** is rendered in this book, with outputs, so you can check your work.

To run notebooks on your own computer:

```bash
git clone https://github.com/kstrm/modeling-environmental-flows.git
cd modeling-environmental-flows
pip install -r requirements.txt
jupyter lab
```
