---
title: "Exercise: Tar River backwater and a buoyant river plume"
---

# Exercise: Tar River Backwater and a Buoyant River Plume

Related lessons: [steady 1D hydraulics and GVF](../../notes/03-steady-1d-hydraulics-gvf.md) and [river mouth plume](../../notes/05-river-mouth-plume.md). The data for problem 2 are in the `Data/` folder next to this page.

**Data provenance.** The files in `Data/` contain values extracted (digitized) from figures in published journal papers, including Strom and Keyvani (2016) and Hetland (2010); they are provided for educational use only. Please cite the original papers when using them, and consult the originals for authoritative values.

**Starter notebook.** [Open `starter.ipynb`](<https://colab.research.google.com/github/kstrm/modeling-environmental-flows/blob/main/03-ode-applications/exercises/tar-river-and-plume/starter.ipynb>) in Colab (or find it next to this page in the repository). The geometry and Manning functions are provided, and the plume data are loaded for you. In Colab, upload the `Data/` folder next to the notebook (or clone the repository). Try each problem before opening the hints at the bottom of this page.

## Problem 1: Depth and velocity in a coastal river

Compute depth and velocity in the Tar River in North Carolina under (1) low discharge and high sea level (a storm surge before the river has had time to swell) and (2) high discharge and normal sea level (a draining landscape after the storm has passed and the surge has fallen).

The reach of interest is the 28 km stretch from Greenville, NC to Washington, NC, where the Tar becomes the Pamlico. The water surface at Washington is essentially tied to sea level. Take the reach to be a trapezoidal channel with bottom width 65 m, side slope $m=2$ (horizontal : vertical), bed slope $S=0.00004$ and Manning's $n=0.04$.

Relevant USGS stations: 02084000 (Tar River at Greenville, NC) and 02084472 (Pamlico River at Washington, NC).

1. What is the normal depth of the reach at $Q=30\ \mathrm{m^3/s}$? Neglect sea level (base level) for now.
2. Take that normal depth to be the typical depth, with the water surface at Washington at 0 m elevation (so the bed there is at $-h_n$). Solve the gradually varied flow equation from Washington upstream to Greenville, and farther if needed, with any numerical method, for:
   1. **High base level:** downstream water surface equal to the normal condition plus a 10 ft storm surge, with $Q=40\ \mathrm{m^3/s}$.
   2. **High discharge:** downstream water surface back at normal sea level, with $Q=200\ \mathrm{m^3/s}$.

   For each of the three conditions (normal, high base level, high discharge), plot (a) the depth $h(x)$, (b) the bed elevation $\eta(x)$ and water surface elevation $y_{elev}(x)$, and (c) the velocity $U(x)$.
3. Take the top of the bank at Greenville to be 2.5 m above the normal water surface. Would either scenario flood Greenville?
4. Compare the velocity along the channel in the two scenarios, using the normal condition as a baseline. Speculate on what might happen to sediment transport and bed morphodynamics.
5. This analysis is simplified. Discuss the largest limitations, and how improving the model might change the outcome.

## Problem 2: Buoyant freshwater discharge into a salty embayment

Solve the layer-averaged conservation equations for the thickness $h(x)$, width $W(x)$, velocity $U(x)$, density $\rho(x)$ and suspended sediment concentration $C(x)$ of a buoyant plume. The equations are those of Strom and Keyvani (2016), *Flocculation in a decaying shear field and its implications for mud removal in near-field river mouth discharges*, as summarized in the [river mouth plume note](../../notes/05-river-mouth-plume.md).

1. Solve the hydraulics (eqs. 4–7 of the paper) with any numerical method, using the inlet conditions provided for the Merrimack and Mississippi rivers (`Data/Merrimack_BC.txt` and `Data/Mississippi_BC.txt`). Compare with the plume data in the folder; that is, reproduce Figure 2 of the paper.
2. Add a conservation equation for the suspended sediment exported to the shelf to predict $C(x)$ (do not include flocculation). Which has the stronger influence on $C(x)$, entrainment of ambient clear water or sediment settling? Initial concentration and particle size are in `Data/Sediment_conditions.txt`.
3. We again simplified a complex system to a set of ODEs. Which assumptions or simplifications most limit the applicability of the model output?

## Hints

Try the problem first. Each hint is hidden until you open it, and the hints go from a gentle nudge to a stronger one.

**Problem 1.1 (normal depth)**

:::{dropdown} Hint
Normal depth is the depth at which Manning's equation, with the bed slope as the friction slope, gives the discharge $Q$. Write $Q_{Manning}(h)-Q$ as a function and find its root with `scipy.optimize.brentq` on a bracket such as $[0.01, 30]$ m.
:::

**Problem 1.2 (backwater profiles)**

:::{dropdown} Hint 1
The equation to integrate is $dh/dx=(S_o-S_f)/(1-Fr^2)$ with $S_f=\left[Qn/(AR^{2/3})\right]^2$ and $Fr^2=Q^2T/(gA^3)$, where $T$ is the top width. The channel is wide and shallow here, so check the Froude number you get at normal depth.
:::

:::{dropdown} Hint 2
Information about the downstream boundary travels upstream, so integrate **from Washington upstream**. If you let $x$ be the distance upstream from Washington, then $dh/dx_{up}=-dh/dx_{down}$. Pass this to `solve_ivp` with `t_span=(0, 28000)`.
:::

:::{dropdown} Hint 3
The bed elevation is $\eta=-h_n+S_o\ x_{up}$ with $h_n$ the normal depth from 1.1 (the bed at Washington sits at $-h_n$). The water-surface elevation is $\eta+h$, and the velocity is $Q/A$. A 10 ft storm surge is about 3.05 m of added downstream depth.
:::

**Problems 1.3 to 1.5**

:::{dropdown} Hint
For flooding, compare your water-surface elevation at Greenville with the bank top, 2.5 m above the *normal* water surface there. Think about which scenario raises the stage farther upstream, and over what distance each backwater effect fades.
:::

**Problem 2.1 (plume hydraulics)**

:::{dropdown} Hint 1
Unknowns: $u$, $h$, $w$, $\Delta\rho$, with $Q=uhw$. Compute the initial density difference from the salinities and temperatures with `rho_cw` in `Data/WaterProperties.py`. The plume equations (A3, A5, A12, A13) are in the [river mouth plume note](../../notes/05-river-mouth-plume.md).
:::

:::{dropdown} Hint 2
The entrainment velocity is $w_e=\delta\ u$, with the constant ratio $\delta$ given in the inlet files as the entrainment velocity ratio. The critical densimetric Froude number in the same file is the condition at lift-off. One way to set the initial plume thickness is to find $h_0$ such that $Fr_d=u_0/\sqrt{g'h_0}$ equals it, with $u_0=Q/(w_0h_0)$.
:::

:::{dropdown} Hint 3
Evaluate $dQ/dx=w_ew$ first, then $d\Delta\rho/dx$, $dw/dx$, $du/dx$ and finally $dh/dx$ (the last depends on the others). Return all four derivatives from one function and integrate with `solve_ivp`. Check your units when comparing with the digitized data (some of the plume data are scaled).
:::

**Problem 2.2 (sediment)**

:::{dropdown} Hint 1
Only settling removes sediment mass from the plume. Entrainment adds clear water, which dilutes $C$ but does not change the sediment mass flux $QC$. This suggests solving for $QC$ (or $C$) with a settling term proportional to $w_sCw$ per unit length, where $w_s$ is the settling velocity.
:::

:::{dropdown} Hint 2
For $62\ \mu$m sand, estimate $w_s$ from Stokes' law and check that the particle Reynolds number is small enough for Stokes' law to apply (it should be below about 1). To compare the two effects, run the model with entrainment turned off, then with settling turned off.
:::
