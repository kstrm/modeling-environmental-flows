---
title: Spatial Discretization and Finite-Difference Schemes
---

# Spatial Discretization and Finite-Difference Schemes

:::{admonition} Learning objectives
:class: tip
After this lesson you should be able to:

- build forward, backward and central differences from Taylor series and state their order of accuracy
- derive a finite-difference stencil by matching Taylor series coefficients
- count grid points and apply one-sided differences at the boundaries
- write a derivative as a matrix operator acting on the grid values
:::

So far we have studied initial value problems, which develop in time or space but have no definite end. As we move toward PDEs we turn to (1) general spatial discretization on a domain with a finite end and (2) boundary value problems. Reference: Chapter 4 of Aref and Balachandar (2018).

## The grid

Consider a domain of length $L$ divided into $N$ segments:

$$x_i=i\,\Delta x,\quad i=0,\ldots,N,\qquad\Delta x=\frac LN,$$

giving $N+1$ grid points (the end points carry the boundary conditions; the rest are the interior).

## Taylor series and three classic derivatives

$$f(x_0+\Delta x)=f(x_0)+\Delta x\,f'(x_0)+\frac{\Delta x^2}{2!}f''(x_0)+O(\Delta x^3)\tag{1}$$

$$f(x_0-\Delta x)=f(x_0)-\Delta x\,f'(x_0)+\frac{\Delta x^2}{2!}f''(x_0)+O(\Delta x^3)\tag{2}$$

We can use these to estimate $f'$, $f''$, $f'''$ from $f(x_0)$, $f(x_0\pm\Delta x)$.

**Forward difference** (solve (1) for $f'$; two-point stencil):

$$f'_j\approx\frac{f_{j+1}-f_j}{\Delta x}=f'_j+\tfrac12\Delta x\,f''_j+O(\Delta x^2)\qquad\text{first-order accurate.}$$

Rewriting (1) as $f(x_0+\Delta x)\approx f(x_0)+\Delta x\,f'(x_0)$ is explicit Euler.

**Backward difference** (solve (2) for $f'$; two-point stencil):

$$f'_j\approx\frac{f_j-f_{j-1}}{\Delta x}=f'_j-\tfrac12\Delta x\,f''_j+O(\Delta x^2)\qquad\text{first-order accurate, like implicit Euler.}$$

**Central difference** ((1) minus (2); three-point stencil):

$$f(x_0+\Delta x)-f(x_0-\Delta x)=2\Delta x\,f'(x_0)+O(\Delta x^3)\;\Rightarrow\;f'_j\approx\frac{f_{j+1}-f_{j-1}}{2\Delta x}=f'_j+\tfrac16\Delta x^2f'''_j+\cdots$$

which is second-order accurate.

In general, the order of accuracy is roughly the number of stencil points minus one. Near the boundaries, where a centered stencil is unavailable, one-sided differences (forward at the first point, backward at the last) are used.

## Building schemes on a general stencil

Seek $f'_j\approx a f_{j-2}+b f_{j-1}+c f_j+d f_{j+1}+e f_{j+2}$ (a five-point stencil). Taylor expanding each term about $x_j$:

$$
\begin{aligned}
\text{RHS}={}&(a+b+c+d+e)f_j+\Delta x(-2a-b+d+2e)f'_j+\frac{\Delta x^2}{2}(4a+b+d+4e)f''_j\\
&+\frac{\Delta x^3}{6}(-8a-b+d+8e)f'''_j+\frac{\Delta x^4}{24}(16a+b+d+16e)f''''_j+O(\Delta x^5).
\end{aligned}
$$

For LHS = RHS we choose the coefficients so that the coefficient of $f'_j$ is 1 and as many other low-order terms as possible vanish.

**Example, three-point stencil for $f'$** ($a=e=0$): the conditions are

$$b+c+d=0,\qquad-b+d=\frac1{\Delta x},\qquad b+d=0,$$

so $d=\dfrac1{2\Delta x}$, $b=-\dfrac1{2\Delta x}$, $c=0$, recovering the central difference $f'_j\approx(f_{j+1}-f_{j-1})/(2\Delta x)$.

**Example, three-point stencil for $f''$** ($a=e=0$): the conditions are

$$b+c+d=0,\qquad-b+d=0,\qquad b+d=\frac2{\Delta x^2},$$

so $b=d=\dfrac1{\Delta x^2}$, $c=-\dfrac2{\Delta x^2}$:

$$f''_j\approx\frac{f_{j-1}-2f_j+f_{j+1}}{\Delta x^2}.$$

This is second-order accurate (the leading error term vanishes by symmetry). In general an $M$-point stencil gives order of accuracy about $M-1$ for the first derivative, and symmetric stencils can do slightly better for the second.

The second derivative is the diffusive term in the advection–diffusion and Navier–Stokes equations. Error analysis (how a scheme responds to sines of different frequency) comes later.

## Implementation: loops, slicing and plotting

For $f(x)=\sin x$ on $[0,6\pi]$ with $N=100$ points, the derivative is estimated with a loop,

```python
import numpy as np

x = np.linspace(0, 6*np.pi, N)
f = np.sin(x)

df = np.zeros(N)
for i in range(N - 1):
    df[i] = (f[i+1] - f[i]) / (x[i+1] - x[i])
df[-1] = (f[-1] - f[-2]) / (x[-1] - x[-2])      # backward difference at the last point
```

or with vector operations and array slicing (no loop):

```python
df_f = np.zeros(N); df_b = np.zeros(N); df_c = np.zeros(N)
df_f[:-1] = (f[1:]  - f[:-1]) / (x[1:]  - x[:-1])     # forward
df_b[1:]  = (f[1:]  - f[:-1]) / (x[1:]  - x[:-1])     # backward
df_c[1:-1] = (f[2:] - f[:-2]) / (x[2:]  - x[:-2])     # central
```

Each is compared with the analytic $\cos x$. The end points are not set by the central difference (they need a one-sided formula or a boundary condition). The notebook ends with a slider that shows how the error of each formula changes with the number of points.

:::{admonition} Hands-on: Classic finite differences and vector operations
:class: note
Compute and plot the three differences for $\sin x$ and compare them with $\cos x$. Work through **[Classic finite differences and vector operations](../../05-pdes/completed/09_ClassicFD.ipynb)** (the completed version, shown in this book), or [open the student version in Colab](<https://colab.research.google.com/github/kstrm/modeling-environmental-flows/blob/main/05-pdes/notebooks/09_ClassicFD.ipynb>) and fill in the blanks yourself.
:::

## Matrix derivative operator

A scheme can be viewed as a mapping from the values of $f$ at the grid points to the values of the derivative at the grid points:

$$f_i^{(p)}=\left[D_p\right]_{im}f_m\quad(\text{repeated index}\Rightarrow\text{sum}),$$

where $[D_p]_{im}$ is the matrix derivative operator. For the central difference ($3$-point stencil) with periodic boundary conditions,

$$
\begin{bmatrix}f'_0\\f'_1\\f'_2\\\vdots\\f'_{N-1}\end{bmatrix}
=\frac1{2\Delta x}
\begin{bmatrix}
0&1&0&0&\cdots&-1\\
-1&0&1&0&\cdots&0\\
0&-1&0&1&\cdots&0\\
&&\ddots&&&\\
1&0&\cdots&0&-1&0
\end{bmatrix}
\begin{bmatrix}f_0\\f_1\\f_2\\\vdots\\f_{N-1}\end{bmatrix},
$$

so that, for example, $f'_1=\dfrac1{2\Delta x}(-f_0+f_2)$. See Section 4.2 of Aref and Balachandar (2018).

## Check your understanding

**1.** A domain is divided into $N$ segments. How many grid points are there?

:::{dropdown} Answer
$N+1$: the two end points (which carry the boundary conditions) and $N-1$ interior points.
:::

**2.** What is the order of accuracy of the forward and central differences?

:::{dropdown} Answer
Forward is first order (leading error $\tfrac12\Delta x f''$); central is second order (leading error $\tfrac16\Delta x^2 f'''$).
:::

**3.** What three-point stencil approximates $f''$?

:::{dropdown} Answer
$f''_j\approx(f_{j-1}-2f_j+f_{j+1})/\Delta x^2$, second-order accurate.
:::

**4.** What do you do at the first and last grid points, where a centered stencil is not available?

:::{dropdown} Answer
Use one-sided differences (forward at the first point, backward at the last) or apply the boundary condition.
:::

**5.** Why do the stencil conditions $b+c+d=0$, $-b+d=1/\Delta x$, $b+d=0$ give the central difference?

:::{dropdown} Answer
They require the $f_j$ and $f''_j$ terms to cancel and the $f'_j$ coefficient to equal 1, which leads to $d=1/(2\Delta x)$, $b=-1/(2\Delta x)$, $c=0$.
:::
