# PSet3 Explained

### Q1,3,5,7

#### Log return

$$
ret = ln(\frac{P_{t+1}}{P_t})
$$

For log return, the final return is 
$$
ret = ln(\frac{P_n}{P_1}) = ln(\frac{P_2}{P_1}) + ln(\frac{P_3}{P_2}) + ... + ln(\frac{P_n}{P_{n-1}})
$$
Annualized Average return
$$
mean\_ret_{annual} = mean\_ret_{daily} * Days
$$
Annualized return volatility
$$
std\_ret_{annual} = std\_ret_{daily}*sqrt(days)
$$

## Q2,4,6,8

Besides the values given, dividends $c=0$.

#### Time to maturity

Calculated based on $d_1$ 
$$
d_1 = \frac{log(S_0/K) + (r - c + \sigma^2/2)T}{\sigma\sqrt{T}}=\frac{(r  + \sigma^2/2)T}{\sigma\sqrt{T}}
$$

#### Calculation of $d_1$ 

Note that for each period, using its own _S_ and _T_
$$
d_i^1 = \frac{log(S_i/K) + (r + \sigma^2/2)T_i}{\sigma\sqrt{T_i}}
$$

#### Calculation of $d_2$

Note that for each period, using its own T
$$
d_i^2 = d_i^1 - \sigma\sqrt{T_i}
$$

#### Calculation of call price $c_i$

Note that for each period's $c_i(S_i,\sigma, T)$, using its own $S_i$, $T_i$, $d^1_i$ and $d^2_i$

 
$$
C_i(S_i, \sigma, T_i) = S_ie^{-cT_i}N(d^1_i) - Ke^{-rT_i}N(d^2_i)
$$
for $N(d)$ is using function _NORM.DIST(d, 0,1,TRUE)_

#### Calculation of Delta

Note that for each period using its own $T_i$
$$
\delta_i = e^{-cTi}N(d^1_i) = N(d^1_i)
$$

#### \# of stocks hold

This refers to number of shares
$$
\#shares_i = \delta_i * \#option_i
$$

#### Self Financing Port Value

This is the part that using the **amount of money earned from selling options, invest into stocks for hedging**, hence

**Initial S.F Port Value**
$$
V_0 = c_0*\#option
$$
Since portfoio is self financing, hence the value of portfolio as markets moves is 
$$
V_{i+1} = V_i + \delta_i(S_{i+1}-S_i + S_ic\Delta t)*\#option + (V_i - \delta_iS_i*\#option)(e^{r\Delta t} - 1)
$$

$$
= V_i + \delta_i(S_{i+1}-S_i)*\#option + (V_i - \delta_iS_i*\#option)(e^{r\Delta t} - 1)
$$

$$
= V_i + HedgingPortRet + CashRet
$$

$$
= V_i + \delta_iS_i*\#option (S_{i+1}/S_i - 1 + c\Delta t) +  (V_i - \delta_iS_i*\#option)(e^{r\Delta t} - 1)
$$

Where $S_i$ is the stock price. 

#### Cash Account

$$
Cash_i = Vi - \#share_i * S_i
$$
