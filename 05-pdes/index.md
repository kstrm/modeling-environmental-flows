---
title: "05 PDEs: advection and diffusion"
---

# PDEs: advection and diffusion

Terminology, model equations, and finite-difference schemes for advection and diffusion, with the stability theory that decides which schemes work.

## Learning goals

- Classify PDEs as linear or nonlinear, homogeneous or not
- Discretize the advection and diffusion equations in space and time
- Use the CFL condition and von Neumann analysis to choose a stable time step
- Recognize numerical diffusion and dispersion, and choose between upwind, Lax-Wendroff and implicit schemes

## Lesson notes

1. [PDEs - Terminology and Model Equations](notes/01-pdes-classification-and-model-equations.md)
2. [The Advection Equation - FTBS and FTCS](notes/02-advection-equation-ftbs-ftcs.md)
3. [Stability, the CFL Condition and von Neumann Analysis](notes/03-stability-cfl-and-von-neumann.md)
4. [Upwind, Lax and Implicit Schemes](notes/04-upwind-lax-and-implicit-schemes.md)

## Notebooks

| Notebook | Open in Colab |
|---|---|
| [09 ClassicFD](completed/09_ClassicFD.ipynb) | [Student version](<https://colab.research.google.com/github/kstrm/modeling-environmental-flows/blob/main/05-pdes/notebooks/09_ClassicFD.ipynb>) |
| [13 SimplePDE Advection](completed/13_SimplePDE_Advection.ipynb) | [Student version](<https://colab.research.google.com/github/kstrm/modeling-environmental-flows/blob/main/05-pdes/notebooks/13_SimplePDE_Advection.ipynb>) |
| [14 AdvectionDiffusion Schemes Stability](completed/14_AdvectionDiffusion_Schemes_Stability.ipynb) | [Student version](<https://colab.research.google.com/github/kstrm/modeling-environmental-flows/blob/main/05-pdes/notebooks/14_AdvectionDiffusion_Schemes_Stability.ipynb>) |

## Exercises

- [Exercise: A kerosene spill (advection-diffusion)](exercises/advection-diffusion-spill/index.md)
