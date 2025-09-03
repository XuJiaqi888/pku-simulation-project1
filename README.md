# Investment Allocation via Simulated Annealing

## Background
An investor has total capital of 1 to be allocated across n companies over a fixed investment horizon. Investing a fraction p_i in company i yields a payoff only when the company’s market value at maturity X_i exceeds a given threshold x_i. Conditional on success (X_i ≥ x_i), the random payoff Y_i is uniformly distributed on [0, X_i]. The allocation vector p = (p_1, ..., p_n) is subject to p_i ≥ 0 and \sum_i p_i = 1.

In this notebook we consider n = 3 with thresholds x_1 = 2, x_2 = 3, and x_3 = 1.

## Model
For i = 1, 2, 3, the maturity value is modeled as

X_i = ( ρ V + sqrt(1 − ρ^2) η_i ) / max(W, 1),

where
- ρ = 0.6 controls the strength of the common factor,
- V ~ Normal(0, 1) is the common market factor,
- η_i ~ Normal(0, i) models firm-specific idiosyncratic risk (variance i),
- W ~ Exponential(rate = 1/0.3) models common market shocks,
- All random variables are independent.

Conditional payoff: Y_i | X_i ~ Uniform(0, X_i). A project generates payoff only if X_i ≥ x_i.

## Objective
We seek the portfolio p that maximizes the risk-adjusted performance (Sharpe-like ratio)

maximize  E[ S(p) ]  where  S(p) = sum_{i=1}^3 p_i Y_i 1{X_i ≥ x_i} / std( sum_{i=1}^3 p_i Y_i 1{X_i ≥ x_i} ).

## Approach
- Monte Carlo simulation to sample (V, W, η_i) and generate (X_i, Y_i).
- Simulated Annealing (SA) to search over p on the simplex { p_i ≥ 0, \sum p_i = 1 }.
- Proposal moves keep allocations on the simplex; temperature schedule controls exploration.

## How to run
1. Install Jupyter:
   - pip: `pip install jupyterlab` (or `pip install notebook`)
2. Launch the notebook and run all cells:
   - `jupyter lab project1.ipynb`  (or `jupyter notebook project1.ipynb`)
3. The notebook simulates the model and applies SA to produce an optimized allocation p.

## Repository structure
- `project1.ipynb`: simulation and optimization notebook
- `README.md`: this document

## Notes
- This repository is for educational and research purposes only and does not constitute investment advice.
