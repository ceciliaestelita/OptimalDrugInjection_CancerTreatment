# Optimal Drug Injection for Cancer Treatment
Constrained nonlinear optimal control of a cell-cycle specific chemotherapy model using ODE solvers and FMINCON in MATLAB

![Status](https://img.shields.io/badge/Status-Complete-green)
![Language](https://img.shields.io/badge/Language-MATLAB-orange)
![Application](https://img.shields.io/badge/Application-Optimal_Control-blue)
![Field](https://img.shields.io/badge/Field-Biomedical_Engineering-purple)

## ⚙️ Methodology
* **Compartmental ODE Modeling (`my_ode.m`):** Implemented coupled differential equations tracking proliferating (`P`) and quiescent (`Q`) cell populations under piecewise-constant drug infusion intervals (`N = 2, 5, 10`) over `T = 30` days.
* **Cost Function Design (`cost.m`):** Coupled `ode45` numerical integration with a terminal objective minimizing final tumor cell count `P(T)` plus cumulative drug toxicity weighted by `μ`.
* **Nonlinear State Constraints (`constraints.m`):** Enforced patient health safety bounds (`P(t) + Q(t) >= ρ` with `ρ = 0.35`) alongside control saturation limits (`u(t) ∈ [0, 1]`) via `fmincon`.
* **Parametric Exploration:** Tested solver convergence across zero and randomized initial guesses, and evaluated control sensitivity across toxicity weights (`μ = 0.001, 0.01, 0.1`).

## 📊 Results
* **Control Granularity (`N`):** Increasing the number of control intervals from `N = 2` to `N = 10` enabled finer dosing modulation, driving `P(T)` lower while keeping total cell count `P + Q` strictly above the `0.35` safety threshold.
* **Impact of Toxicity Weight (`μ`):** Higher `μ` values penalized cumulative drug usage, shifting the optimal strategy toward delayed or pulsed dosing rather than continuous maximum infusion.
* **Initialization Robustness:** Comparing zero vs. random initial guesses highlighted local minima behavior in non-convex trajectory optimization, demonstrating the importance of multi-start strategies.
