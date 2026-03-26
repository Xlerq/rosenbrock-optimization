# Rosenbrock Optimization in R

Implementation of the Rosenbrock derivative-free search method for constrained optimization of a two-variable objective function on the domain `[-1, 1] x [-1, 1]`.

The project compares three parameter settings:
- `(alpha = 2, beta = 1/2)`
- `(alpha = 3, beta = 1/3)`
- `(alpha = 4, beta = 1/4)`

Each configuration is tested on 100 random starting points for:
- minimization of `f(x, y)`
- maximization of `f(x, y)` via minimization of `-f(x, y)`

---

## Objective function

```text
f(x, y) = x^2 - y^2 - cos(1.8*pi*x) - cos(1.6*pi*(y - 0.5)) + 3

The optimization is constrained to the square:

(x, y) ∈ [-1, 1] × [-1, 1]

Outside the feasible domain, the constrained objective returns Inf, which prevents the algorithm from leaving the search region.

Project idea

This is a derivative-free optimization project.
Instead of computing gradients, the algorithm probes the objective function directly and adapts its step sizes depending on success or failure.

The implementation includes:

adaptive step expansion after successful moves
step contraction and sign reversal after failed moves
basis rotation using Gram-Schmidt orthogonalization
stopping based on sufficiently small step size or iteration limit
Experiment setup

The experiment includes:

100 random starting points sampled from [-1, 1] × [-1, 1]
3 parameter configurations
separate runs for minimization and maximization
classification into global optimum, local optimum, or no convergence
exported results in raw, aggregated, and trajectory form
Main results
Global minimum
value: approximately 0.388670
location: approximately (0.000000, -0.815765)
Global maximum
value: approximately 5.314836
location: approximately (-0.592916, -0.115828)
due to symmetry, an equivalent maximum also appears near (0.592916, -0.115828)
Key observations
minimization often converges to a local minimum
maximization reaches the global maximum much more often
larger alpha generally increases computational cost
the starting point strongly affects the final result
Output interpretation

The exported results are organized into three logical groups:

_wyniki
Raw run-by-run outputs for every start and parameter setting
_wartości_średnie
Aggregated averages and counts for global/local outcomes
_wykresy
Contour plots with optimization trajectories for a selected starting point

Useful metrics:

L.wywołań = number of objective function evaluations
L.zmian bazy = number of basis rotations
Repository structure
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
Folder meaning
report/ – R Markdown report
results/ – generated outputs and Excel results
docs/ – supporting documentation and notes
src/ – core algorithm code
scripts/ – runnable scripts
figures/ – exported plots for README/report
data/ – input or generated auxiliary data
Reproducibility

The original implementation uses a fixed random seed so that the experiment can be reproduced consistently.

Planned runnable entry point:

Rscript scripts/run_experiment.R
Why this project matters

This project is not just about finding one number.

Because the objective function is highly non-convex and contains multiple local extrema, the main point is to analyze how the Rosenbrock method behaves under:

different starting points
different step parameters
minimization vs maximization
computational cost vs convergence quality
Status

Current repository version contains:

the original report in R Markdown form
the generated Excel output
project documentation and presentation notes
an organized structure prepared for modular refactoring into src/ and scripts/

Further cleanup will separate the algorithm, experiment loop, plotting, and export logic into standalone R modules.
