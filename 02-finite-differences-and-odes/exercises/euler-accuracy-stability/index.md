---
title: "Exercise: Accuracy and stability of Euler and Runge-Kutta"
---

# Exercise: Accuracy and Stability of Euler and Runge-Kutta

Related lessons: [Euler's method](../../notes/01-eulers-method.md), [accuracy, Taylor series and stability](../../notes/02-accuracy-taylor-series-and-stability.md), [Runge-Kutta methods](../../notes/03-runge-kutta-methods.md).

**Starter notebook.** [Open `starter.ipynb`](<https://colab.research.google.com/github/kstrm/modeling-environmental-flows/blob/main/02-finite-differences-and-odes/exercises/euler-accuracy-stability/starter.ipynb>) in Colab (or find it next to this page in the repository). Cells marked TODO are left for you; the scaffolding (imports, error metric, timing helper) is provided. Try each problem before opening the hints at the bottom of this page.

**1.** Consider the ODE

$$\frac{dy}{dt}=\lambda\,(y-\sin t)+\cos t.$$

1. Find the general analytic solution.
2. Solve the equation with the explicit Euler method for $\lambda=-0.2$ and $y(0)=1/\sqrt2$ from $t=0$ to $2\pi$. Use time steps $\Delta t=\pi/10,\ \pi/20,\ \pi/40$ and $\pi/80$. Plot each result against the analytic solution and report the mean squared error for each time step.
3. Determine analytically the condition for stability. Check it empirically and show that your condition holds when you run the calculations.
4. Repeat the analysis for $\lambda=-10$.

**2.** Apply the 4th-order Runge-Kutta scheme to the same equation with $\lambda=-0.2$ and $\Delta t=\pi/10$.

1. Compare its accuracy with the Euler results from problem 1. Where does it sit relative to them?
2. Time each Euler calculation and the Runge-Kutta calculation. How do the computation times compare?
3. Try other values of $\Delta t$ and $\lambda$ with Runge-Kutta and record your observations, particularly relative to Euler.

**3.** Convince yourself that accuracy depends not only on the time or space step but also on the shape of the function being computed. Demonstrate your reasoning in whatever way you see fit.

**4.** Which scheme does SciPy's `solve_ivp` use by default to solve a single ODE or a system of ODEs? How does it choose its step size, and how does it compare with your fixed-step Runge-Kutta calculation?

## Hints

Try the problem first. Each hint is hidden until you open it, and the hints go from a gentle nudge to a stronger one.

**Problem 1.1 (analytic solution)**

:::{dropdown} Hint 1
The equation is linear. Split it into a particular solution plus the solution of the homogeneous part, $y'=\lambda y$.
:::

:::{dropdown} Hint 2
Try $y_p=\sin t$ as a particular solution: substitute it into $\lambda(y-\sin t)+\cos t$ and see what remains. Then add $Ce^{\lambda t}$ and use $y(0)=1/\sqrt2$ to find $C$.
:::

**Problem 1.2 (Euler and the error)**

:::{dropdown} Hint
Build the time array with `np.arange(0, 2*np.pi + dt/2, dt)` so the last point lands on $2\pi$. For $\lambda=-0.2$, the mean squared error should fall by a factor of about 4 each time $\Delta t$ is halved. Why 4 and not 2? (Think about what Euler's order of accuracy says about the error itself, and then what squaring does.)
:::

**Problem 1.3 and 1.4 (stability)**

:::{dropdown} Hint 1
Write $y_{i+1}$ in terms of $y_i$ and collect the terms that multiply $y_i$. The forcing terms do not change whether errors grow or decay.
:::

:::{dropdown} Hint 2
The factor multiplying $y_i$ is $1+\lambda\Delta t$; errors decay only if its magnitude is below 1. Tabulate $|1+\lambda\Delta t|$ for each step size and compare with what you see in the plots. For $\lambda=-10$ the steps $\pi/10$ and $\pi/20$ fall on opposite sides of the limit.
:::

**Problem 2 (Runge–Kutta and timing)**

:::{dropdown} Hint
The four slope evaluations are in the [Runge–Kutta note](../../notes/03-runge-kutta-methods.md). A single run takes well under a millisecond, so time many repeats and divide, as the starter notebook does. For a fair comparison, find the Euler step size that matches the RK4 error and compare the costs at *equal accuracy*, not equal step.
:::

**Problem 3 (shape of the function)**

:::{dropdown} Hint
Keep $\Delta t$ fixed and change the function, for example $dy/dt=\cos(\omega t)$ for several values of $\omega$. How does the error depend on $\omega\Delta t$?
:::

**Problem 4 (`solve_ivp`)**

:::{dropdown} Hint
Look at the `method` argument in the `solve_ivp` documentation to find the default. Compare the step sizes it chose (`np.diff(sol.t)`) with your fixed step, and compare `sol.nfev` with the number of slope evaluations your RK4 used ($4\times$ the number of steps).
:::
