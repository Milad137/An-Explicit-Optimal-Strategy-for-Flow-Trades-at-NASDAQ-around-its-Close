### This reaserch is based on the paper, An Explicit Optimal Strategy for Flow Trades at NASDAQ around its Close, published by Christoph Frei and Chad Yan.
<br>
<br>
NASDAQ trading hours and types are as following
<img src="https://i.ibb.co/m0QsRfB/Untitled.png" alt="Untitled" border="0">
<br>
<br>

### Objective:

**A trader wants to place an order with the amount of W before NASDAQ closes, how should the trader split the order volume to gain the highest profit?**
<br>
<br>
A trader wants to place a buy order of $W$ units. They can split the order into $v_1,v_2,...,v_T$ with $\sum_{t=1}^T v_t = W$ where $v_1,v_2,...,v_{T-1}$ are the volumes of orders submitted to the open market and $v_T$ is submitted to the closing auction.
<br>
<br>
For a given initial price $P_0$ , the prices are modelled by 
<br>
$
\begin{equation*}
P_t = P_{t-1} + Z_t +\beta {v_t} \; \; \; \; for \; \;  t∈{1,...,τ−1,τ+1...,T −1} \\
P_τ = P_{τ-1} + Z_t +\alpha {N} +\beta {v_t} \\
P_T = P_{T-1} + Y +\beta {v_t}
\end{equation*}
$
<br>
• $Z_t$ modelling the stock price fluctuations in the open market <br>
• $Y$, modelling the fluctuations from the last price in the open market to the auction price <br>
• $N = N+v_T$ is the auction imbalance <br>
• $α>0$ reflects the impact of the auction imbalance on stock prices <br>
• $β>0$ is the coefficient of temporary market impact by trader's order <br>
• $T$ the closing time of the auction <br>
• Let $τ <T$ be the time of the initial imbalance announcement <br>

-------------------------
The optimal strategy based on modern portfolio theory
is given by

<br>
$
\begin{equation*}
v_1 = \frac{\alpha W}{2(\beta + m_1 + \sum_{i=2}^{τ-1} m_i p_i)} \\
v_t = p_t v_1 \; \; \; \; for \; \;  t= 2, 3,...,τ−1 \\
v_k = 0 \; \; \; \; for \; \;  t= τ,τ+1,...,T-1  \\
v_T = W - (1+\sum_{i=2}^{τ−1} p_i)v_1 \\
where \\
m_t = (T-t)\lambda {\sigma^2}_Z + \lambda {\sigma^2}_Y + \lambda {\alpha}^2 {\sigma^2}_N + \alpha \\
p_t = (\frac{\lambda {\sigma}^2_Z}{\beta} + 1 - x_-)  \frac{{{x^t}_+}}{{x^2}_+-1} + (\frac{\lambda {\sigma}^2_Z}{\beta} + 1 - x_+)  \frac{{{x^t}_-}}{{x^2}_--1} \\
x_{\pm} = 1 + \frac{\lambda {\sigma}^2_Z}{2\beta} \pm \sqrt{\frac{\lambda {\sigma}^2_Z}{\beta}(1+\frac{\lambda {\sigma}^2_Z}{4 \beta})}
\end{equation*}
$
<br>
<br>

---
### Code Breakdown
---
1. Flowchart

2. Research Notes

3. Library and Input

4. Retrieve Data

5. Frei_Chan_Weights

6. Fre-Chan Parameter Sensitivity Analysis

7. Performance Visualization

---
### Analysis:
Based on Frei-Chan strategy, order weights are calculated. In [Frei-Chan Weight Distribution for Last 30 Minutes Figure](#fig1), it can be seen that the last weight takes up most of order volume. In order to analyze the effect of Frei-Chai parameters, this last weight is used as an indicator to demonstrate the importance of 6 main parameters.<br>
As depicted in [Parameter Impact on Frei-Chan Last Weight Figure](#fig2), it can be inferred that $α$, $\lambda$, $\sigma^2_N$ and $\sigma^2_Z$ have the highest impact on volume distribution.<br>
To find optimum parameters, it is assumed that each day, two trades are placed, one using Freo-Chan method and the other using market close time method. The accumulated price difference of these two methods is calculated for selected stocks in 2017 to generate [Frei-Chan Performace Charts](#fig3). Based on this performace charts, follwoing values are selected for parameters:
<br>
$
\begin{equation*}
{\alpha} = 1e-6 \\
{\beta} = 1e-6 \\
{\lambda} = 1e-3 \\
{{\sigma}^2_N} = 1e9 \\
{{\sigma}^2_Z} = 1e-9 \\
{{\sigma}^2_Y} = 1e-9 
\end{equation*}
$
<br>

Using optimal parameters of Frei-Chan strategy, charts for Daily and Cumulative Performance Relative to Stock Close Price (%) have been plotted. It can be seen from [Daily and Cumulative Performace Charts](#fig4) that compared to unbroken order strategy at market close time that the strategy improves the performance.<br>
<br>
As demonstrated in [Performance Table](#fig5), on average 55% of times, Frei-Chan outperforms traditional approach with an average of 0.022% improvement on each trading day.
