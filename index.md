---
title: Modeling of Environmental Flows
---

# Modeling of Environmental Flows

How do we predict the movement of water and of the substances it carries (sediment, salt, nutrients, contaminants), and the changes that take place in the water column and at the bed? This course introduces the numerical methods used to answer that question in rivers, estuaries and other natural environments, and gives you hands-on practice coding simple flow and transport problems yourself.

The first half builds understanding and skill with simplified systems: finite-difference theory applied to ODEs and PDEs, with an emphasis on writing your own solvers in Python. The second half moves to more complex settings: 1D unsteady hydraulics (Saint-Venant equations), 2D shallow water modeling, and 3D modeling with freely available tools such as HEC-RAS and Delft3D.

## Who this is for

Graduate and advanced undergraduate students in civil and environmental engineering, geoscience and related fields. You should be comfortable with the differential forms of the equations of motion and transport. No prior programming experience is assumed; the first module gets you started with Python and Jupyter.

## How the course is organized

Each module contains lesson notes, notebooks to work through, and exercises. The notebooks and exercises appear **inline**, at the point in the lessons where they apply, so you can simply keep clicking *Next* at the bottom of each page and move through the material in order. Each module's home page also lists everything in one place.

| Module | Topics |
|---|---|
| 00 Getting started | Python, Jupyter notebooks, first steps with arrays and plots |
| 01 Governing equations | Conservation laws, averaging, laminar vs turbulent flow, model resolution |
| 02 Finite differences and ODEs | Euler method, accuracy, stability, Runge-Kutta, ODE systems |
| 03 ODE applications | Mixing tanks, gradually varied flow, stratified flow and river plumes |
| 04 Boundary value problems | Linear systems, Couette-Poiseuille flow, Blasius boundary layer |
| 05 PDEs | Advection, diffusion, advection-diffusion, CFL stability, implicit schemes |
| 06 1D unsteady hydraulics | Saint-Venant equations, explicit and implicit schemes, morphodynamics (Exner equation) |

Modules on HEC-RAS (1D and 2D) and Delft3D (3D) will follow. Two reference pages help along the way: [Notation](notation.md) and the [Glossary](glossary.md). If you are teaching from the course, see the [Notes for instructors](instructors.md).

## Using the notebooks

Every lecture notebook comes in two versions. The **student version** has blanks for you to fill in and lives in each module's `notebooks/` folder in the [GitHub repository](https://github.com/kstrm/modeling-environmental-flows). The **completed version** is rendered in this book, with outputs, so you can check your work.

### Run the code

There are three ways to run the code, from quickest to most flexible:

1. **On the page.** On pages that contain code, press the power button at the top of the page. After a minute or two a free, temporary Jupyter session (hosted by Binder) starts and you can edit and run the cells right here. Nothing is saved, so copy anything you want to keep. If the session does not start (the free service is sometimes busy), use option 2 or 3.
2. **In Google Colab.** Each lesson links to the student version of its notebook. Colab needs only a Google account and lets you save your work to Drive.
3. **On your own computer,** which is best for the larger exercises and the capstone project.

To run notebooks on your own computer:

```bash
git clone https://github.com/kstrm/modeling-environmental-flows.git
cd modeling-environmental-flows
pip install -r requirements.txt
jupyter lab
```
