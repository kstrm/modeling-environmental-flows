---
title: Systems of ODEs
---

# Systems of ODEs

A system of ODEs is handled exactly like a single equation; there are just more calculations. For

$$\frac{dy_1}{dx}=f_1(x,y_1,y_2),\qquad\frac{dy_2}{dx}=f_2(x,y_1,y_2),$$

RK4 is applied to each equation, with every slope evaluation using the current estimates of **all** the variables:

$$y^{1}_{i+1}=y^{1}_i+\frac{\Delta x}{6}\left(K^1_1+2K^1_2+2K^1_3+K^1_4\right),\qquad y^{2}_{i+1}=y^{2}_i+\frac{\Delta x}{6}\left(K^2_1+2K^2_2+2K^2_3+K^2_4\right).$$

Companion notebooks: [Method 1 (explicit coefficients)](../completed/05_ODESys-Method1-RK4.ipynb), [A note on multidimensional arrays](../completed/06_A-note-on-multidimensional-arrays.ipynb), [Method 2 (arrays)](../completed/07_ODESys-Method2-RK4-array.ipynb) and [Method 3 (`solve_ivp`)](../completed/08_ODESys-Method3-solve_ivp.ipynb).

## Example: predator–prey (rabbits and foxes)

$$\frac{dR}{dt}=aR-bRF,\qquad\frac{dF}{dt}=-lF+kRF,$$

where $R$ and $F$ are the rabbit and fox populations, $a$ is the base birth rate of rabbits, $b$ the prey factor, $l$ the fox base diminishing rate and $k$ the feeding rate. With $a=0.5$, $b=0.01$, $l=1$, $k=0.005$, $R_0=500$, $F_0=100$ and $\Delta t=0.01$, the populations oscillate, and the $R$–$F$ phase plot is a closed loop.

### Method 1: write out each RK coefficient

Build up from the single-equation loop: define `fR` and `fF`, then compute `K1R, K1F, K2R, K2F, ...` explicitly, each using the intermediate values of both variables.

```python
for i in range(N - 1):
    K1R = fR(t[i],           y1[i],                 y2[i])
    K1F = fF(t[i],           y1[i],                 y2[i])
    K2R = fR(t[i] + 0.5*dt,  y1[i] + 0.5*dt*K1R,    y2[i] + 0.5*dt*K1F)
    K2F = fF(t[i] + 0.5*dt,  y1[i] + 0.5*dt*K1R,    y2[i] + 0.5*dt*K1F)
    K3R = fR(t[i] + 0.5*dt,  y1[i] + 0.5*dt*K2R,    y2[i] + 0.5*dt*K2F)
    K3F = fF(t[i] + 0.5*dt,  y1[i] + 0.5*dt*K2R,    y2[i] + 0.5*dt*K2F)
    K4R = fR(t[i] + dt,      y1[i] + dt*K3R,        y2[i] + dt*K3F)
    K4F = fF(t[i] + dt,      y1[i] + dt*K3R,        y2[i] + dt*K3F)
    y1[i+1] = y1[i] + (dt/6)*(K1R + 2*K2R + 2*K3R + K4R)
    y2[i+1] = y2[i] + (dt/6)*(K1F + 2*K2F + 2*K3F + K4F)
```

### Method 2: arrays

Store the unknowns in one 2D array `y` with shape `(2, N)` (row 0 rabbits, row 1 foxes), and let `f` return a 1D array of both slopes. The RK4 loop is then written once, identical to the single-equation case, with `y[:, i]` passing all variables at index `i`:

```python
def f(t, y):
    return np.array([a*y[0] - b*y[0]*y[1],
                    -l*y[1] + k*y[0]*y[1]])

y = np.zeros((2, N))
y[:, 0] = [R_0, F_0]
for i in range(N - 1):
    K1 = f(t[i],           y[:, i])
    K2 = f(t[i] + 0.5*dt,  y[:, i] + 0.5*dt*K1)
    K3 = f(t[i] + 0.5*dt,  y[:, i] + 0.5*dt*K2)
    K4 = f(t[i] + dt,      y[:, i] + dt*K3)
    y[:, i+1] = y[:, i] + (dt/6)*(K1 + 2*K2 + 2*K3 + K4)
```

## Indexing multidimensional arrays

In `x[a, b, c]` the first index selects which array (matrix), the next the row, and the last the position within the row. For an array of shape `(3, 4)` (3 sets of arrays of length 4), `x2[2, 0]` is the first value of the third row and `x2[1, :]` is the whole second row. For a `(3, 4, 5)` array, `x3[0, 0, 3]` is the 4th value in the first row of the first matrix, and `x3[1, :, -1]` is the last column of the second matrix. Useful properties are `.ndim`, `.shape` and `.size`. For paired $x,y$ values on a grid, use `np.mgrid` or `np.meshgrid`, e.g. to evaluate and contour a function of two variables. For more, see the *Python Data Science Handbook*, "The Basics of NumPy Arrays".

## Method 3: SciPy's `solve_ivp`

`scipy.integrate.solve_ivp` solves the same system with a library routine. The function takes the independent variable first and the state second, exactly like the hand-written RK4 above, and returns the slopes.

```python
import numpy as np
from scipy.integrate import solve_ivp

def df(t, ic):
    R, F = ic[0], ic[1]
    dR = a*R - b*R*F
    dF = -l*F + k*R*F
    return [dR, dF]

t = np.arange(0, 50, 0.01)
ic = [R_0, F_0]
sol = solve_ivp(df, (0, 50), ic, t_eval=t)    # sol.t: times, sol.y: shape (2, len(t))
```

By default `solve_ivp` uses an adaptive Runge-Kutta method (`RK45`, Dormand-Prince): it chooses its own internal step size to meet the tolerances `rtol` and `atol`, and `t_eval` only controls where the solution is reported. Other methods are chosen with `method=` (`RK23`, `DOP853`, and the implicit `Radau` and `BDF` for stiff problems). The result object holds `sol.t`, `sol.y` and diagnostics such as `sol.nfev`, the number of function evaluations.

Note the array layout is the same as Method 2: `sol.y[0]` is rabbits and `sol.y[1]` is foxes, one row per variable. Use `ax.plot(t, sol.y.T)` to plot both at once. The older `odeint` interface, which takes `f(y, t)` and returns the transpose, is still found in a lot of code, but new code should use `solve_ivp`.
