# 📘 Vector Autoregression (VAR) Model

## 🔹 Introduction
**Vector Autoregression (VAR)** is a multivariate time series model that captures the **linear interdependencies** among multiple variables.  
Unlike univariate autoregressive (AR) models, VAR treats **all variables as endogenous**.  
It is widely used in **econometrics, finance, and macroeconomic forecasting**.

---

## 🔹 Mathematical Formulation

Suppose we have \(k\) time series variables, collected in a vector:

$$
\mathbf{y}_t =
\begin{bmatrix}
y_{1t} \\
y_{2t} \\
\vdots \\
y_{kt}
\end{bmatrix}
$$

A **VAR(p)** model of order \(p\) is defined as:

$$
\mathbf{y}_t = \mathbf{c} + A_1 \mathbf{y}_{t-1} + A_2 \mathbf{y}_{t-2} + \dots + A_p \mathbf{y}_{t-p} + \mathbf{u}_t
$$

where:
- $\mathbf{y}_t \in \mathbb{R}^k$: vector of variables at time $t$  
- $\mathbf{c} \in \mathbb{R}^k$: constant/intercept vector  
- $A_i \in \mathbb{R}^{k \times k}$: coefficient matrices for lag $i$  
- $\mathbf{u}_t \sim \mathcal{N}(0, \Sigma)$: vector of white-noise errors with covariance matrix $\Sigma$  

---

## 🔹 Example (2-variable VAR(1))

If we have **GDP growth** \((g_t)\) and **Inflation** \((\pi_t)\), then a VAR(1) looks like:

\begin{equation}
\begin{bmatrix}
g_t \\
\pi_t
\end{bmatrix}
=
\begin{bmatrix}
c_1 \\
c_2
\end{bmatrix}
+
\begin{bmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{bmatrix}
\begin{bmatrix}
g_{t-1} \\
\pi_{t-1}
\end{bmatrix}
+
\begin{bmatrix}
u_{1t} \\
u_{2t}
\end{bmatrix}
\end{equation}

Here:
- \(g_t\) depends on its own lag \((g_{t-1})\) and lagged inflation \((\pi_{t-1})\)  
- \(\pi_t\) depends on lagged GDP \((g_{t-1})\) and lagged inflation \((\pi_{t-1})\)  

---

## 🔹 Stationarity Condition

For the VAR to be stable, the **roots of the characteristic polynomial** must lie outside the unit circle:

\[
\det \left( I_k - A_1 z - A_2 z^2 - \cdots - A_p z^p \right) \neq 0 \quad \text{for} \quad |z| \leq 1
\]

---

## 🔹 Forecasting

One-step ahead forecast:

\[
\hat{\mathbf{y}}_{t+1} = \mathbf{c} + A_1 \mathbf{y}_{t} + A_2 \mathbf{y}_{t-1} + \cdots + A_p \mathbf{y}_{t-p+1}
\]

---

## 🔹 Impulse Response Function (IRF)

An **Impulse Response Function (IRF)** shows how a shock in one variable affects the future values of all variables.

If \(\mathbf{u}_t = e_j\) (a one-unit shock in variable \(j\)), the response at horizon \(h\) is:

\[
IRF(h, j) = \frac{\partial \mathbf{y}_{t+h}}{\partial u_{jt}}
\]

---

## 🔹 Forecast Error Variance Decomposition (FEVD)

FEVD quantifies how much of the variance in the forecast error of variable \(i\) at horizon \(h\) is explained by shocks to variable \(j\).

\[
\text{FEVD}_h(i,j) = \frac{\text{Var} \left( \text{error in } y_{i,t+h} \text{ due to } u_j \right)}{\text{Total Var} \left( \text{error in } y_{i,t+h} \right)}
\]

---

## ✅ Summary

- VAR generalizes univariate AR models to **multivariate systems**.  
- Each variable is a function of **its own lags** and **lags of all other variables**.  
- Tools: **Stationarity tests (ADF)**, **Granger causality**, **Impulse Response Functions (IRF)**, **FEVD**, **SVAR**.  
