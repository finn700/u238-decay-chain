# U-238 Radioactive Decay Chain Simulation

A numerical simulation of the Uranium-238 decay chain using the Bateman equations, 
built in Python. The chain progresses through 14 radioactive isotopes before 
reaching stable Lead-206, spanning timescales from microseconds to billions of years.

## Overview

This project models how the quantity of each isotope in the U-238 decay series 
evolves over time, starting from pure U-238. It solves a system of 15 coupled 
ordinary differential equations (the Bateman equations) numerically and 
demonstrates the emergence of **secular equilibrium** across the chain.

## Physics Background

Each isotope in a decay chain is governed by:
dN_i/dt = λ_(i-1) * N_(i-1) - λ_i * N_i

where production comes from the decay of the parent isotope, and loss comes 
from the isotope's own decay. The decay constant λ is calculated from each 
isotope's half-life:
λ = ln(2) / half-life

The U-238 chain is numerically **stiff** — decay constants span over 20 orders 
of magnitude, from U-238 (half-life 4.47 billion years) to Po-214 (half-life 
164 microseconds). This requires an implicit solver (SciPy's Radau method) 
rather than standard explicit methods.

## Key Result: Secular Equilibrium

The simulation demonstrates that secular equilibrium emerges in stages, governed 
by each isotope's half-life relative to its neighbours:

- By ~10,000 years, fast-decaying isotopes (Th-234, Pa-234) are already in 
  equilibrium with U-238, while the rest of the chain lags behind, rate-limited 
  by the longer-lived U-234 (half-life 245,500 years).
- By ~2 million years, the entire 14-isotope chain converges to a single 
  equilibrium activity matching U-238.

This explains why naturally occurring uranium ore is radioactive well beyond 
what U-238 alone would produce — every daughter product contributes roughly 
equal activity at equilibrium.

## What's in the Notebook

- `u238_simulation.ipynb` — full simulation, including:
  - Half-life data and decay constant calculations
  - Bateman equation setup
  - Numerical solution via `scipy.integrate.solve_ivp`
  - Plots of isotope abundance and activity over time
  - Demonstration of secular equilibrium at different timescales

## How to Run

1. Clone this repository
2. Install dependencies:
pip3 install numpy scipy matplotlib jupyter
3. Open `u238_simulation.ipynb` in Jupyter or VS Code
4. Run all cells in order

## Data Sources

Half-life data sourced from the National Nuclear Data Center (NNDC), 
Brookhaven National Laboratory — https://www.nndc.bnl.gov

## Author

Finn Coleman — Nuclear and Radiation Physics student, Adelaide University
