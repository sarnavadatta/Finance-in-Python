The Black-Scholes model is a mathematical formula used to calculate the theoretical price of European-style options. It helps traders determine a fair price for an options contract by considering factors like the underlying stock's price, the option's strike price, the time until expiration, volatility, and interest rates.

---

## The Black-Scholes Formula 📜

The model provides separate formulas for calculating the price of a European **call option** ($C$) and a European **put option** ($P$).

The price of a **call option** is calculated as:
$$C(S_t, t) = S_t N(d_1) - K e^{-r(T-t)} N(d_2)$$

The price of a **put option** is calculated as:
$$P(S_t, t) = K e^{-r(T-t)} N(-d_2) - S_t N(-d_1)$$

### Formula Components

The terms $d_1$ and $d_2$ are given by:
$$d_1 = \frac{\ln(\frac{S_t}{K}) + (r + \frac{\sigma^2}{2})(T-t)}{\sigma \sqrt{T-t}}$$
$$d_2 = d_1 - \sigma \sqrt{T-t}$$

Here's a breakdown of each variable:

* **$C(S_t, t)$**: Price of the call option.
* **$P(S_t, t)$**: Price of the put option.
* **$S_t$**: Current price of the underlying asset (e.g., stock price).
* **$K$**: Strike price of the option.
* **$T-t$**: Time to expiration of the option, expressed in years.
* **$r$**: Risk-free interest rate (annual).
* **$\sigma$** (sigma): Volatility of the underlying asset's returns.
* **$N(d)$**: The cumulative standard normal distribution function, which gives the probability that a standard normal random variable will be less than or equal to $d$. In this context, $N(d_2)$ can be interpreted as the risk-neutral probability that the option will be exercised (i.e., finish in-the-money).

---

## The Greeks (Risk Sensitivities) 🇬🇷

"The Greeks" are a set of risk measures that indicate how sensitive an option's price is to changes in certain parameters. They are the partial derivatives of the option price function.

### Delta ($\Delta$)

**Delta** measures the rate of change of the option price with respect to a change in the underlying asset's price. It ranges from 0 to 1 for call options and -1 to 0 for put options.

* **Call Delta**: $\Delta_C = \frac{\partial C}{\partial S} = N(d_1)$
* **Put Delta**: $\Delta_P = \frac{\partial P}{\partial S} = N(d_1) - 1$

### Gamma ($\Gamma$)

**Gamma** measures the rate of change of an option's delta with respect to a change in the underlying asset's price. It indicates how much the delta will change for a $1 move in the underlying.

* **Gamma (for both call and put)**: $\Gamma = \frac{\partial^2 V}{\partial S^2} = \frac{N'(d_1)}{S_t \sigma \sqrt{T-t}}$
    * Where $N'(x) = \frac{1}{\sqrt{2\pi}} e^{-\frac{x^2}{2}}$ is the standard normal probability density function.

### Theta ($\Theta$)

**Theta** measures the rate of change of the option price with respect to the passage of time. It's often called "time decay" and is usually negative for long options.

* **Call Theta**: $\Theta_C = -\frac{S_t N'(d_1) \sigma}{2 \sqrt{T-t}} - r K e^{-r(T-t)} N(d_2)$
* **Put Theta**: $\Theta_P = -\frac{S_t N'(d_1) \sigma}{2 \sqrt{T-t}} + r K e^{-r(T-t)} N(-d_2)$

### Vega ($\mathcal{V}$)

**Vega** measures the rate of change of the option price with respect to a change in the volatility of the underlying asset. Note that Vega is not a real Greek letter.

* **Vega (for both call and put)**: $\mathcal{V} = \frac{\partial V}{\partial \sigma} = S_t \sqrt{T-t} N'(d_1)$

### Rho ($\rho$)

**Rho** measures the rate of change of the option price with respect to a change in the risk-free interest rate.

* **Call Rho**: $\rho_C = \frac{\partial C}{\partial r} = K (T-t) e^{-r(T-t)} N(d_2)$
* **Put Rho**: $\rho_P = \frac{\partial P}{\partial r} = -K (T-t) e^{-r(T-t)} N(-d_2)$

This model and its Greeks form the foundation for options pricing, hedging, and risk management in modern quantitative finance.


