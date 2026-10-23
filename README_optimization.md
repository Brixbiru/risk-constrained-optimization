# Portfolio Optimization with Risk Constraint

Finds portfolio weights across five stocks that maximize expected return while keeping portfolio variance under 2.5%. Two methods are implemented and compared: projected gradient descent and the penalty method.

## Problem

Maximize expected return, subject to:

- weights are non-negative and sum to 1
- portfolio variance ≤ 0.025 (2.5%)

The script minimizes the objective `f(w) = -μᵀw + (λ/2)wᵀΣw` with λ = 1.

## Methods

**1. Gradient descent with projection**
Takes gradient steps, then projects the weights back onto the simplex (non-negative, sum to 1) after each step.

**2. Penalty method**
Adds penalty terms for violating the sum, non-negativity, and variance constraints. The penalty parameter ρ starts at 1 and is multiplied by 5 each outer iteration until the constraints are satisfied.

## Inputs

| Stock         | Expected return |
|---------------|-----------------|
| Tech_A        | 12%             |
| Finance_B     | 10%             |
| Energy_C      | 8%              |
| Healthcare_D  | 11%             |
| Consumer_E    | 9%              |

The covariance matrix is defined directly in the script.

## Results

| Stock         | Gradient descent | Penalty method |
|---------------|------------------|----------------|
| Tech_A        | 59.38%           | 33.38%         |
| Finance_B     | 6.52%            | 18.83%         |
| Energy_C      | 0.00%            | 6.89%          |
| Healthcare_D  | 34.10%           | 27.69%         |
| Consumer_E    | 0.00%            | 13.21%         |
| **Expected return** | 11.53%    | 10.67%         |
| **Risk (std dev)**  | 15.21%    | 11.11%         |
| **Variance**        | 2.312%    | 1.234%         |

Gradient descent gives the higher return but concentrates the portfolio in two stocks. The penalty method spreads the weight across all five stocks and has lower risk.

## Running

Requires Python 3 with NumPy, pandas, and Matplotlib.

```bash
python3 Gradient_optimization.py
```

The script prints the results and saves `portfolio_optimization_results.png` with six plots: weights, objective convergence, gradient norm, risk-return trade-off, constraint violation, and penalty growth.

## Notes

- Gradient descent uses the full 2,000 iterations and does not reach the convergence tolerance. Its solution happens to satisfy the variance limit, but the method does not enforce it.
- The penalty method converges after 10 outer iterations, and its solution is well under the 2.5% limit.
- The interpretation text printed by the script is written in advance and is not computed from the results.
