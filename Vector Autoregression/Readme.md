# Vector Autoregression (VAR) Model

## Introduction
Vector Autoregression (VAR): is a statistical model used to capture the linear relationships among multiple time series variables. Unlike univariate autoregressive models, VAR treats all variables as endogenous, meaning each variable is modeled as a function of its own past values and the past values of all other variables in the system.
## Key features
- Multivariate: Handles multiple time series simultaneously.
- Lag Structure: Each variable depends on lagged values of itself and others.
- Applications: Widely used in macroeconomics, finance, and forecasting.

## Mathematical form

A **VAR($p$)** model of order $p$ is defined as: 
 $ \mathbf{y}_t$ = $\mathbf{c} + A_1 \mathbf{y}_{t-1} + A_2 \mathbf{y}_{t-2} + \dots + A_p \mathbf{y}_{t-p} + \mathbf{u}_t $


where:

- $\mathbf{y}_t \in \mathbb{R}^k$: vector of variables at time $t$  
- $\mathbf{c} \in \mathbb{R}^k$: constant/intercept vector  
- $A_i \in \mathbb{R}^{k \times k}$: coefficient matrices for lag $i$  
- $\mathbf{u}_t \sim \mathcal{N}(0, \Sigma)$: vector of white-noise errors with covariance matrix $\Sigma$

---

