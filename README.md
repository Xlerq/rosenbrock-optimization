# Rosenbrock Optimization in R

R implementation of the Rosenbrock derivative-free search method for constrained optimization of a two-variable objective function on the domain `[-1, 1] × [-1, 1]`.

## Overview

This project studies how the Rosenbrock direct search method behaves on a non-convex two-dimensional objective function with multiple local extrema.

The experiment compares three parameter settings:

- `alpha = 2`, `beta = 1/2`
- `alpha = 3`, `beta = 1/3`
- `alpha = 4`, `beta = 1/4`

Each configuration is tested on 100 random starting points for:

- minimization of `f(x, y)`
- maximization of `f(x, y)` via minimization of `-f(x, y)`

## Objective function

```text
f(x, y) = x^2 - y^2 - cos(1.8*pi*x) - cos(1.6*pi*(y - 0.5)) + 3
```

Subject to:

```text
(x, y) ∈ [-1, 1] × [-1, 1]
```

Outside the feasible domain, the constrained objective returns `Inf`, which prevents the algorithm from leaving the search region.

## Method

The implementation is based on the Rosenbrock derivative-free search method and includes:

- adaptive step expansion after successful moves
- step contraction and sign reversal after failed moves
- basis rotation using Gram-Schmidt orthogonalization
- stopping based on sufficiently small step size or iteration limit

## Experiment setup

The experiment includes:

- 100 random starting points sampled from `[-1, 1] × [-1, 1]`
- 3 parameter configurations
- separate runs for minimization and maximization
- classification into global optimum, local optimum, or no convergence

## Main results

### Global minimum

- value: approximately `0.388670`
- location: approximately `(0.000000, -0.815765)`

### Global maximum

- value: approximately `5.314836`
- location: approximately `(-0.592916, -0.115828)`
- due to symmetry, an equivalent maximum also appears near `(0.592916, -0.115828)`

## Key observations

- minimization often converges to a local minimum
- maximization reaches the global maximum much more often
- larger `alpha` generally increases computational cost
- the starting point strongly affects the final result

## Example trajectories

The plots below show the Rosenbrock method for the same parameter setting  
`alpha = 3`, `beta = 1/3`, for both optimization goals.

<p align="center">
  <img src="./figures/trajectory-max-a3-b13.png" alt="Maximization trajectory for alpha=3, beta=1/3" width="48%">
  <img src="./figures/trajectory-min-a3-b13.png" alt="Minimization trajectory for alpha=3, beta=1/3" width="48%">
</p>

<p align="center">
  <em>Left: maximization. Right: minimization. Same parameters, different search behavior.</em>
</p>

## Repository structure

```text
.
├── README.md
├── .gitignore
├── data/
├── docs/
├── figures/
├── report/
├── results/
├── scripts/
└── src/
```

## Run

The current full implementation is preserved in `report/report.Rmd`.

A standalone command-line entry point in `scripts/run_experiment.R` is planned as part of the ongoing refactor.
## Current contents

This repository currently contains:

- the original R Markdown report
- generated Excel results
- supporting PDF documentation and notes
- a cleaned project structure prepared for modular refactoring

## Next steps

Planned cleanup includes:

- moving the core algorithm into `src/`
- separating experiment logic into `scripts/`
- exporting figures to `figures/`
- making the project fully reproducible from the command line
