# Kalman Filter: 
A Kalman filter is a statistical tool that helps you estimate the “true value” of something that you can’t observe directly.
It does this by combining:
- What you expect (based on a model of how things should move)
- What you see (noisy data or market observations)

Think of it as a “smart averaging machine” that constantly updates as new data comes in.

## Mathematical Formulation: Setup

The Kalman Filter estimates the **hidden state** $x_t$ of a system given **noisy observations** $z_t$.  

We assume a **linear Gaussian state-space model**.

### State Transition (Process Model)

$$
x_t = F x_{t-1} + B u_t + w_t
$$

- $x_t$ : hidden state vector at time \(t\)  
- $F$ : state transition matrix  
- $B u_t$ : optional control input (can be zero)  
- $w_t \sim \mathcal{N}(0, Q)$ : process noise  

### Observation Model

$$
z_t = H x_t + v_t
$$

- $z_t$ : observation vector at time $t$  
- $H$ : observation matrix  
- $v_t \sim \mathcal{N}(0, R)$ : measurement noise  

---

## Kalman Filter Equations

### Prediction Step

$$
\hat{x}_{t|t-1} = F \hat{x}_{t-1|t-1} + B u_t
$$

$$
P_{t|t-1} = F P_{t-1|t-1} F^\top + Q
$$

### Update Step

$$
y_t = z_t - H \hat{x}_{t|t-1} \quad \text{(innovation)}
$$

$$
S_t = H P_{t|t-1} H^\top + R \quad \text{(innovation covariance)}
$$

$$
K_t = P_{t|t-1} H^\top S_t^{-1} \quad \text{(Kalman gain)}
$$

$$
\hat{x}_{t|t} = \hat{x}_{t|t-1} + K_t y_t
$$

$$
P_{t|t} = (I - K_t H) P_{t|t-1}
$$

---

## Interpretation

- **Prediction step:** Forecast next state using the model  
- **Update step:** Correct forecast using observation  
- **Kalman gain $K_t$:** Balances trust between model and observation  

---

## Example: 1D Stock Price with Trend

State vector:

$$
x_t = 
\begin{bmatrix}
p_t \\ v_t
\end{bmatrix}
$$

- $p_t$ : true hidden price  
- $v_t$ : hidden trend (velocity)  

State transition:

$$
x_t = 
\begin{bmatrix}
1 & 1 \\
0 & 1
\end{bmatrix} x_{t-1} + w_t
$$

Observation:

$$
z_t = [1 \quad 0] x_t + v_t
$$

- Only price is observed; trend is hidden  
- Process noise $w_t$ smooths the state  
- Measurement noise $v_t$ models observation error
