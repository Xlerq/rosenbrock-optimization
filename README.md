# Rosenbrock Optimization in R

Implementation of the Rosenbrock direct search method for constrained optimization
of a two-variable objective function on the domain [-1, 1] x [-1, 1].

The project compares three parameter settings:
- (alpha = 2, beta = 1/2)
- (alpha = 3, beta = 1/3)
- (alpha = 4, beta = 1/4)

Each configuration is tested on 100 random starting points for both minimization
and maximization.

## Project overview

The optimized objective function is:

f(x, y) = x^2 - y^2 - cos(1.8 * pi * x) - cos(1.6 * pi * (y - 0.5)) + 3

The optimization is constrained to the square:
[-1, 1] x [-1, 1]

Outside the domain, the constrained objective returns `Inf`, which prevents the
algorithm from leaving the feasible region.

## Method

This project uses the Rosenbrock direct search method, a derivative-free optimization
algorithm based on:
- adaptive step expansion after success,
- step contraction and direction reversal after failure,
- basis rotation using Gram-Schmidt orthogonalization,
- stopping when the step size becomes sufficiently small.

Maximization is performed by minimizing `-f(x, y)`.

## Experiment setup

The experiment includes:
- 100 random starting points sampled from `[-1, 1] x [-1, 1]`,
- 3 `(alpha, beta)` parameter settings,
- separate runs for minimization and maximization,
- result classification into global optimum, local optimum, or no convergence.

## Results summary

Observed global minimum:
- approximately `0.388670`
- near `(0.000000, -0.815765)`

Observed global maximum:
- approximately `5.314836`
- near `(-0.592916, -0.115828)` and symmetrically `(0.592916, -0.115828)`

Main observations:
- minimization often converges to a local minimum rather than the global one,
- maximization reaches the global maximum much more often,
- increasing `alpha` generally increases computational cost,
- the starting point strongly affects the final result.

## Repository structure

- `report/` – R Markdown report
- `results/` – Excel output and generated results
- `docs/` – supporting PDF documentation and notes
- `src/` – core algorithm code
- `scripts/` – runnable scripts
- `figures/` – exported plots
- `data/` – input data / generated starts

## How to run

Once the project is fully split into modules, the experiment should be runnable with:

```bash
Rscript scripts/run_experiment.R
