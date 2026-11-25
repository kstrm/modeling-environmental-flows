---
title: "Exercise: Accuracy and stability of Euler and Runge-Kutta"
---

# Exercise: Accuracy and Stability of Euler and Runge-Kutta

Related lessons: [Euler's method](../../notes/01-eulers-method.md), [accuracy, Taylor series and stability](../../notes/02-accuracy-taylor-series-and-stability.md), [Runge-Kutta methods](../../notes/03-runge-kutta-methods.md).

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

**4.** Which scheme does SciPy's `odeint` use to solve a single ODE or a system of ODEs?
