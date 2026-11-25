---
title: "Exercise: Tar River backwater and a buoyant river plume"
---

# Exercise: Tar River Backwater and a Buoyant River Plume

Related lessons: [steady 1D hydraulics and GVF](../../notes/03-steady-1d-hydraulics-gvf.md) and [river mouth plume](../../notes/05-river-mouth-plume.md). The data for problem 2 are in the `Data/` folder next to this page.

**Data provenance.** The files in `Data/` contain values extracted (digitized) from figures in published journal papers, including Strom and Keyvani (2016) and Hetland (2010); they are provided for educational use only. Please cite the original papers when using them, and consult the originals for authoritative values.

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
