## 📘 Black-Scholes Option Pricing Model

The **Black-Scholes Model** is used to estimate the fair price of European call and put options. It assumes the underlying asset follows a **geometric Brownian motion** with constant volatility and interest rate.

### 🧮 Pricing Formula

#### European Call Option:
```math
C = S_0 \cdot N(d_1) - K \cdot e^{-rT} \cdot N(d_2)
```

#### European Put Option:
```math
P = K \cdot e^{-rT} \cdot N(-d_2) - S_0 \cdot N(-d_1)
```

Where:

```math
d_1 = \frac{\ln\left(\frac{S_0}{K}\right) + \left(r + \frac{\sigma^2}{2}\right)T}{\sigma \sqrt{T}}, \quad
d_2 = d_1 - \sigma \sqrt{T}
```

---

### 📌 Parameter Definitions

| Symbol       | Meaning                                                                 |
|--------------|-------------------------------------------------------------------------|
| \( C \)      | Price of the **Call** option                                            |
| \( P \)      | Price of the **Put** option                                             |
| \( S_0 \)    | Current price of the underlying asset                                   |
| \( K \)      | Strike price                                                            |
| \( T \)      | Time to maturity (in years)                                             |
| \( r \)      | Risk-free interest rate (annualized)                                    |
| \( \sigma \) | Volatility of the underlying asset (standard deviation)                 |
| \( N(d) \)   | CDF of the standard normal distribution                                 |
| \( \ln \)    | Natural logarithm                                                       |

---

## 📉 The Greeks (Sensitivities)

The **Greeks** measure sensitivity of the option price to various factors.

### Delta \( \Delta \)

Measures the rate of change of the option price with respect to changes in the underlying asset's price.

- **Call Option**:
  ```math
  \Delta_{\text{call}} = N(d_1)
  ```

- **Put Option**:
  ```math
  \Delta_{\text{put}} = N(d_1) - 1
  ```

---

### Gamma \( \Gamma \)

Measures the rate of change of Delta with respect to changes in the underlying asset's price (second derivative).

```math
\Gamma = \frac{N'(d_1)}{S_0 \cdot \sigma \sqrt{T}} = \frac{e^{-d_1^2/2}}{S_0 \cdot \sigma \sqrt{2\pi T}}
```

---

### Vega \( \nu \)

Measures sensitivity to volatility.

```math
\text{Vega} = S_0 \cdot N'(d_1) \cdot \sqrt{T}
```

> Same for both calls and puts.

---

### Theta \( \Theta \)

Measures the sensitivity of the option price to the passage of time (time decay).

- **Call Option**:
  ```math
  \Theta_{\text{call}} = -\frac{S_0 \cdot N'(d_1) \cdot \sigma}{2\sqrt{T}} - rK e^{-rT} N(d_2)
  ```

- **Put Option**:
  ```math
  \Theta_{\text{put}} = -\frac{S_0 \cdot N'(d_1) \cdot \sigma}{2\sqrt{T}} + rK e^{-rT} N(-d_2)
  ```

---

### Rho \( \rho \)

Measures sensitivity to the risk-free interest rate.

- **Call Option**:
  ```math
  \rho_{\text{call}} = K T e^{-rT} N(d_2)
  ```

- **Put Option**:
  ```math
  \rho_{\text{put}} = -K T e^{-rT} N(-d_2)
  ```

---

## 🧠 Assumptions

- Efficient markets (no arbitrage)
- No dividends (or adjusted)
- European-style options (only exercisable at maturity)
- Constant risk-free rate and volatility
- Lognormal distribution of asset prices

---

This model and its Greeks form the foundation for options pricing, hedging, and risk management in modern quantitative finance.


