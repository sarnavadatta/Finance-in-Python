The Binomial Option Pricing model is a method for valuing options that uses a discrete-time framework. It creates a "binomial tree" to map out all the possible paths the underlying asset's price could take over the life of the option. By working backward from the option's expiration date, it calculates the option's value at each step, ultimately determining its current theoretical price. This model is particularly useful for valuing **American-style options** due to its ability to check for early exercise at each node.

---

## The Mathematical Model 🌳

The model breaks down the time to expiration into a number of discrete time intervals, or steps. In each step, the asset's price is assumed to either move up by a certain factor ($u$) or down by a certain factor ($d$).

### 1. Defining the Price Movement

The up and down factors are calculated based on the asset's volatility and the length of a time step:

* **Up factor ($u$)**: $u = e^{\sigma \sqrt{\Delta t}}$
* **Down factor ($d$)**: $d = e^{-\sigma \sqrt{\Delta t}} = \frac{1}{u}$

Where:
* **$\sigma$** (sigma): Volatility of the underlying asset.
* **$\Delta t$**: The length of one time step, calculated as $\Delta t = \frac{T}{n}$.
* **$T$**: The total time to expiration (in years).
* **$n$**: The number of steps in the binomial tree.

### 2. Risk-Neutral Probability

The model doesn't use the real-world probability of an up or down move. Instead, it uses a **risk-neutral probability** ($p$), which is the probability of an up-move that would make the expected return of the stock equal to the risk-free rate.

* **Risk-neutral probability ($p$)**: $p = \frac{e^{r \Delta t} - d}{u - d}$
* The probability of a down-move is then simply $(1-p)$.

Where:
* **$r$**: The risk-free interest rate.

### 3. Valuing the Option

The valuation process starts at the final nodes of the tree (at expiration) and works backward to the present.

**A. Value at Expiration (Final Nodes)**

At the expiration date ($T$), the value of the option is its intrinsic value.

* **Call Option**: $C_n = \max(0, S_n - K)$
* **Put Option**: $P_n = \max(0, K - S_n)$

Where:
* **$S_n$**: The price of the underlying asset at a final node.
* **$K$**: The strike price of the option.

**B. Value at Intermediate Nodes (Working Backward)**

For each preceding node, the option's value is the discounted expected value of the option from the two possible future nodes.

* **Option Value**: $C = e^{-r \Delta t} [p C_u + (1-p) C_d]$

Where:
* **$C_u$**: The option's value at the next step if the price moves up.
* **$C_d$**: The option's value at the next step if the price moves down.

For **American options**, you would also check for early exercise at each node:
* **American Call**: $C_{amer} = \max(S_{node} - K, e^{-r \Delta t} [p C_u + (1-p) C_d])$

### 4. General Formula

The price of a European option at time $t=0$ can be summarized by a single formula:

$$C_0 = e^{-rT} \sum_{i=0}^{n} \binom{n}{i} p^i (1-p)^{n-i} \times \max(0, S_0 u^i d^{n-i} - K)$$

Where:
* **$\binom{n}{i}$**: The binomial coefficient, "n choose i", representing the number of paths with exactly $i$ up-moves.
* **$S_0$**: The initial price of the underlying asset.

---

## Relation to the Black-Scholes Model 🔗

The Binomial model can be seen as a discrete-time approximation of the continuous-time Black-Scholes model. As the number of time steps ($n$) in the binomial tree increases towards infinity, the result of the Binomial model converges to the result of the Black-Scholes model.

* **Foundation**: The Cox, Ross, and Rubinstein (CRR) method for setting $u$ and $d$ (as shown above) is specifically designed to make the variance of the log-returns in the binomial tree match the variance in the geometric Brownian motion process that underpins Black-Scholes.
* **Flexibility**: The primary advantage of the Binomial model is its flexibility. It can easily value **American options** and other exotic options with complex features, which is much more difficult with the standard Black-Scholes formula.
