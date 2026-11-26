---
title: Notes for instructors
---

# Notes for instructors

This page is for anyone teaching from the course. Everything here is a suggestion to adapt to your own calendar and students.

## How the material is organized

Each lesson note is followed in the table of contents by the notebooks and exercises that belong to it, so a class meeting can follow the book from one page to the next. Every lecture notebook exists in two versions:

- the **completed version**, with outputs, is part of the book and serves as the worked example;
- the **student version** (in each module's `notebooks/` folder) has blanks to fill in and opens in Colab from the link in the lesson.

The exercises have problem statements. The Euler, Tar River and spill exercises also have starter notebooks with `TODO` stubs and hints. Lesson notes include short self-check questions with answers in dropdowns, and each module page lists learning goals.

## Suggested pacing

The table assumes meetings of about 75 minutes. Adjust it to your term.

| Module | Lesson notes | Suggested meetings | Main activity |
|---|---|---|---|
| 00 Getting started | 1 | 1 | Set up Python and Jupyter; work through the intro notebook |
| 01 Governing equations | 2 | 2 | Discussion of the model hierarchy and the CFD reading guide |
| 02 Finite differences and ODEs | 6 | 5 to 6 | Euler, stability, RK4, systems, `solve_ivp`, spatial differences |
| 03 ODE applications | 5 | 4 | Tank, gradually varied flow, stratified flow, plume model |
| 04 Boundary value problems | 2 | 2 to 3 | Relaxation (Poiseuille–Couette) and shooting (Blasius) |
| 05 PDEs | 4 | 4 to 5 | Advection and diffusion schemes, CFL, von Neumann analysis |
| 06 1D unsteady hydraulics | 4 | 3 to 4 | Saint-Venant, explicit and implicit schemes, Exner equation |

That is roughly 21 to 25 meetings, leaving room for a midterm review, project work and the modules on HEC-RAS and Delft3D when they are added.

## Demonstrate, assign, or leave for self-study

- **Good for live demonstration:** the Euler stability notebook (sweep the step size and watch growth, oscillation and smooth decay), the solver comparison in the `solve_ivp` notebook, FTBS against FTCS in the advection notebook, and the scheme comparison for advection–diffusion. The effect is visible within a minute and starts a discussion.
- **Good to assign:** building RK4 for a system, the relaxation and shooting notebooks, and the exercises. Students need to write the loop themselves before the vectorized version makes sense, and the course shows loops first for that reason.
- **Good for self-study:** the Python background notebook, the note on multidimensional arrays, and the Adams–Bashforth–Moulton note.

## Exercises

| Exercise | Module | What it practices |
|---|---|---|
| Python basics (first homework) | 00 | Markdown and LaTeX, NumPy and Matplotlib, loops, and a normal-depth solver for a trapezoidal channel |
| Accuracy and stability of Euler and Runge–Kutta | 02 | Order of accuracy and the stability limit, measured |
| Tar River backwater and a buoyant river plume | 03 | Gradually varied flow in a coastal river, and an integral plume model using digitized literature data |
| A kerosene spill (advection–diffusion) | 05 | Comparing the analytic solution with finite-difference schemes, with truncation error and stability limits for each |
| Capstone project ideas | 06 | An open-ended project combining the methods |

## Solutions

Worked solutions to the exercises are not part of this repository. The completed lecture notebooks are worked examples of each method, and each exercise includes hints. If you adopt an exercise, write your own solution and test it against the starter notebook, so the starter and your solution stay in step.

## Keeping it working

- A GitHub Actions workflow re-runs every completed notebook from scratch with the pinned versions in `requirements.txt` on each relevant change, so a broken notebook shows up as a failed check.
- To update library versions, change the pins in `requirements.txt` and in `binder/environment.yml` (a check fails if the two differ), then confirm the notebook check passes.
- To adapt the course, fork the repository and edit `myst.yml`, which holds the table of contents. Please keep the license notices and credit the source (see the license section of the home page).
- Corrections and suggestions are welcome as GitHub issues.

## Citing

A `CITATION.cff` file in the repository gives a ready-made citation, and GitHub shows it in the "Cite this repository" panel.
