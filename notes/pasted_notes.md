# Pasted reference notes (from email bodies)

Cleaned excerpts from `hevangel@yahoo.com` emails where text was copy-pasted.

## 11. technical studies

Technical Studies
The following topics explain how to use and interpret the technical analysis GP offers.
For information on how to browse for and add a technical study to your chart: Displaying Technical Studies.
For video tutorials on technical studies: Videos.
Note: This section is continually updated with additional technical study information.
ADMA (Adaptive Moving Average)
Aroon
Asymmetrical Volatility Bands
Average True Range
Bollinger Bands
Commodity Channel Index
Directional Movement Index
GM Calculations
EFMF Calculations
Interpreting an EFMF Study
Fear and Greed
Fisher Transform
Hurst Exponent
Ichimoku
MACD (Moving Average Convergence/Divergence)
MAE (Moving Average - Envelopes)
MDI (McGinley Dynamic Indicator)
MLR (Moving Linear Regression)
MLRR (Moving Linear Regression - R-Squared)
MLRS (Moving Linear Regression - Slope)
MOM (Momentum)
Psychological Line
PTPS (Parabolic Studies)
RMI (Relative Momentum Index)
RSI (Relative Strength Index)
ROC (Rate of Change)
SMA (Simple Moving Average)
Smoothed Moving Average
Spearman Indicator
Stochastics
Triangular Moving Average
Trender
Ultimate Oscillator
Variable Moving Average
Weighted Moving Average
WLPR (Williams %R)
Z-Score
ADMA (Adaptive Moving Average)
ADMA is an exponential moving average (EMA) where the smoothing factor (i.e., calculation period) adapts to trend strength and market volatility by incorporating the efficiency ratio (ER). It was introduced by Perry Kaufman and is sometimes referred to as the Adaptive Moving Average (AMA) or KAMA.
The ER is calculated over one period, while separate fast/slow periods are used to calculate fast/slow smoothing factors that determine the speed of reaction of the EMA. When the market moves sideways or is very volatile, the slow period dominates; whereas, when the market is strongly trending, the fast period takes over.
The AMA Period refers to the period used to calculate the efficiency ratio, while the Fast/Slow periods are used to calculate the Fast Smoothing Factor (FastSF) and Slow Smoothing Factor (SlowSF) that determine the speed of reaction of the AMA.
The Average Smoothing Factor (ASF) is calculated as: (ER * (FastSF - SlowSF) + SlowSF), will tend to use the FastSF period when price is efficiently trending and the SlowSF period when price is moving sideways or is very volatile. The final AMA Smoothing Factor is ASF squared.
Signals
Similar to any moving average study, the points of interest are indicated when price crosses above/below the variable moving average:
If price crosses above the variable moving average, a buy signal is triggered (long position).
If price crosses below the variable moving average, a sell signal is triggered (short position).
Price can also bounce off the ADMA, which can act as levels of support and resistance.
To display an ADMA chart, enter GPO ADMA <GO>.
Calculations
Step 1: Efficiency Ratio (ER)
1. Change = ABS[Close - Close>>Period]
2. Change = Volatility Sum = SUM[ABS(Close - (Close >> 1) ), Period]
Step 2: Smoothing Constant (SC)
SC = [ER * (Fastest SC - Slowest SC) + Slowest SC]^2
Step 3: ADMA (Adaptive Moving Average)
ADMA = ADMA>>1 + SC * (C - ADMA >> 1)
BQL Example
=BQL("AAPL US Equity", "adma(close=px_last(), ma_period=14, fast_period=2, slow_period=30)")
Return to Top
Aroon
Aroon [Oscillator] is a trend-following technical indicator that uses aspects of the Aroon Indicator ("Aroon Up" and "Aroon Down") to gauge the strength of a current trend and the likelihood that it will continue. The Aroon Oscillator is calculated by subtracting Aroon Up from Aroon Down.
In Sanskrit, the term "aroon" means "dawn's early light." It was so named because of its propensity to alert traders to developing trends in the markets. Like dmi() ( Directional Movement Index ), the Aroon Oscillator is used as an indication of whether or not a particular security or index is trending or non-trending, as well as the current direction of the trend and its strength.
Like many oscillators, the Aroon line fluctuates between -100 and 100. The farther away from zero, the stronger the trend. Readings above zero indicate that an uptrend is present, while readings below zero indicate that a downtrend is present.
Readings above 70 in either the Aroon Up or Aroon Down lines is considered an indication of a strongly trending market. As an Aroon Up or Down breaks through 50 to the downside, it is a sign that the trend is losing steam. The Aroon Up line is calculated by analyzing the number of bars since the highest level in a given period. Aroon Down is the opposite: the number of bars since the lowest level in a given period. When the Up and Down lines are moving lower in tandem, it is often a sign of a non-trending consolidation period.
Non-trading days are omitted from the calculation.
Signals
Readings of Aroon Line above 70 in either one of these lines is considered an indication of a strongly trending market. As an Aroon-Up or Aroon-Down breaks through 50 to the downside, it is sign that the trend is losing steam.
The crossover between Aroon-Up and Aroon-Down can indicate a reversal in trend.
If Aroon-Up reaches 100, and stays between 70 and 100, while Aroon-Down remains between 0 and 30, a new uptrend can be underway.
If Aroon-Down reaches 100, and stays between 70 and 100, while Aroon-Up remains between 0 and 30, a new downtrend can be underway
When the Up & Down lines are moving lower in tandem, it is often a sign of a non-trending, consolidation period.
To display an Aroon chart, enter GCP AROON <GO>.
In the chart below, the Aroon indicator is used with the periodicity of 25 (default is 10). The consolidation period is displayed in blue, where the Aroon-Up and Aroon-Down are moving together in tandem. The uptrend period is in green, when Aroon-Up keeps close to 100, while Aroon-Down keeps close to 0. You can also see the downtrend period when Aroon-Down keeps close to 100, while Aroon-Up keeps close to 0.
Calculations
Aroon Up = ((N Periods - (Days Since N Period High)) / N Periods) x 100
Aroon Down = ((N Periods - (Days Since N Period Low) / N Periods) x 100
Aroon Oscillator = Aroon Up - Aroon Down
BQL Example
=BQL("GOOG US Equity", "dropna(aroon(dates=range(-1Y, 0D), per=D, period=25))"
Return to Top
Asymmetrical Volatility Bands
Asymmetrical Volatility Bands (AVB) is a technical indicator that captures a directional bias of the volatility inherent in many markets. To calculate the band values, the standard deviation of positive directional changes and the standard deviation of negative directional changes are added and subtracted, respectively, from the moving average. To account for the directional bias within the market, the bands can each be shifted by a different factor.
The moving average length and price, number and length of standard deviations, upper and lower band factors are all user adjustable parameters within the study.
When you do not override the parameters, the study returns the asymmetrical volatility bands, calculated using a five-day moving average of the given security's last price. The upper band is derived from one standard deviation in positive directional changes over the last 250 trading days and multiplied by a factor of one, while the lower band is derived from one standard deviation in negative directional changes over the last 250 trading days and multiplied by a factor of zero.
Non-trading days are omitted from the calculation.
Signals
A break above or below the bands can signal the start of a new trend as indicated by the green curve on the chart below.
Conversely, during a period of sideways movement, the band can indicate mean reversion points as marked by the red arrows on the chart below.
Calculations
Moving Average = Simple Average of n Periods
Upper Band = Moving Average + Upper Band Factor * Standard Deviation Up
Lower Band = Moving Average - Lower Band Factor * Standard Deviation Down
BQL Example
=BQL("EUR Curncy", "asvb(close=px_last(), ma_period=14)")
Return to Top
Average True Range
Average True Range ("ATR") is a technical indicator that measures volatility by decomposing an entire range of values for a security over a specified period. First, the true range indicator is measured, which is the greatest of the following: current high less the current low, the absolute value of the current high less the previous close, or the absolute value of the current low less the previous close. ATR is then calculated as a moving average of the true range.
In the chart below, the ATR strategy is backtested using a Sample Strategy in TSIG <GO>. The short trading signal (the red icon on the chart) is triggered when the five-day ATR spikes above 0.5 and when the closing price is lower than the opening price. Using a daily chart for the last one year on General Electric, we can see in the statistics on the right how there were three short signals for this period, averaging a 16.84% average 20-day return.
Calculations
The True Range is the greatest of the following:
Today's high minus today's low.
The absolute value of today's high minus yesterday's close.
The absolute value of today's low minus yesterday's close.
BQL Example
=BQL("AAPL US Equity", "atr(dates=range(-1M,0D), period=14, ma_type=EXPONENTIAL, per=D, fill=prev)"
Return to Top
Bollinger Bands
Bollinger Bands is a technical indicator that plots lines above and below the moving average of a series of values at a specified number of standard deviations. It is used to identify periods of high and low volatility, as well as periods when prices are at extreme and possibly unstable levels.
This is a mean-reversion technique that consists of a moving average and two bands above and below. Most use a standard deviation of 2.0, which means the security will trade between the bands 95% of the time, and a moving average period of 20 days. Bollinger Bands are typically used together with other indicators, such as Relative Strength Index (RSI).
When the markets become more volatile, the bands widen (move further away from the average), and during less volatile periods, the bands contract (move closer to the average). The tightening of the bands is often used by technical traders as an early indication that the volatility is about to increase sharply.
Bollinger Bands is one of the most popular technical analysis techniques. The closer the prices move to the upper band, the more overbought the market, and the closer the prices move to the lower band, the more oversold the market.
Non-trading days are omitted from the calculation.
Signals
Stock price continually touching the lower Bollinger Band indicates oversold condition. A buy signal is usually triggered when the stock price crosses above the upper band.
Stock price continually touching the upper Bollinger Band indicates overbought condition. A sell signal is usually triggered when the stock price crosses above the upper band.
Contraction between the two Bollinger Bands indicates a period of low volatility and potential sign of future increased volatility and possible trading opportunities. Expansion between the two Bollinger Bands indicates a period of high volatility and potential sign of future decreased volatility. Contraction and expansion periods usually alternate.
Calculations
Upper Band: UBB = BollMA+UB Factor*StdDeviation of Price-BollMA
Lower Band: LBB = BollMA-LB Factor*StdDeviation of Price-BollMA
Moving Average: BollMA = N Period Simple Moving Average of Price
Bandwidth: BollW =100 * ((UBB - LBB) / BollMA)
%B: %B = (Price - LBB) / (UBB - LBB)
Where:
The default for Price is Close. Other choices are: Open, High, Low, Mid, HLC Average, OHLC Average, True High, True Low, True Mid, True HLC Average, True OHLC Average
Upper Band Factor: UB Factor = # of Standard Deviations. Default=2
Lower Band Factor: LB Factor = # of Standard Deviations. Default=2
BOLL Period: N Period = For daily, N=days; weekly, N=weeks. The default is 20. BOLL omits non trading days from computations.
BQL Example
=BQL("SPX Index", "boll().upperband, boll().lowerband, boll().average","fill=prev")
Return to Top
Commodity Channel Index
Commodity Channel Index ("CMCI") is a technical indicator that measures the variation of a security's price from its statistical mean. The CMCI can be used to identify possible divergences that may indicate a forthcoming trend for a given security.
A CMCI that falls below -100 indicates an oversold condition. Similarly, a CMCI that rises above 100 indicates an overbought condition. A buy signal is triggered when the indicator crosses -100 from below, while a sell signal is triggered when the indicator crosses 100 from above.
Non-trading days are omitted from the calculation.
Signals
A CMCI that falls below -100 indicates an oversold condition. Similarly, a CMCI that rises above 100 indicates an overbought condition.
A buy signal is triggered when the indicator crosses -100 from below, while a sell signal is triggered when the indicator crosses 100 from above.
Calculations
CMCI = (HLC3 - N Period Simple MA of HLC3) / (0.015 * N Period Mean Deviation of HLC3)
Where:
HLC3 = (High + Low + Close) / 3
N Period= Number of data points to use;
For daily, N=days; for weekly, N=weeks, etc.
BQL Example
=BQL("VOD LN Equity", "dropna(cmci(close=px_last(), dates=range(2020-08-01, 2020-08-14), per=D, period=14))")
Return to Top
Directional Movement Index
Directional Movement Index (DMI) is a technical indicator that reveals the directional movement of a security using today's high and low prices relative to the previous day's high and low prices. By comparing various moving averages, the indicator helps you determine if prices are trending or simply producing noise.
In addition, the ADX value is a measure of the strength of the trend regardless of the trend direction; the higher the value of ADX, the stronger the trend. An ADX value greater than 25 generally suggests that the market is trending, and a value less than 20 indicates no trending. The DMI period defaults to 14 trading days but can be customized.
Signals
Calculations
+DMI = 100 * WSMA(+DM) / ATR
-DMI = 100 * (N Period Smoothed MA of -DM) / ATR
ADX = 100 * (N Period Smoothed MA of DX)
ADXR[i] = ( ADX[i] + ADX[i - N] ) / 2
Average True Range (ATR) = N Period Smoothed Moving Average of True Range;
True Range = Max(Today's High, Previous Close) - Min(Today's Low, Previous Close)
Directional Index (DX) = 100 * abs((+DMI)-(-DMI))/((+DMI)+(-DMI))
Positive Directional Movement:
+DM = if UpMove > DownMove and UpMove > 0, then +DM = UpMove, else +DM = 0
Negative Directional Movement:
-DM = if DownMove > UpMove and DownMove > 0, then -DM = DownMove, else -DM = 0
UpMove = Today's High - Yesterday's High
DownMove = Yesterday's Low - Today's Low
Wilder's Smoothed Moving Average (WSMA) of value V of period N is defined as:
WSMA[N] = Sum(V,1:N) / N
Sum(V,1:N) is the sum of the first N values of V. i.e. the initial value = the simple MA of the first N points.
WSMA[i] = ( V[i] + (N-1) * WSMA[i - 1] ) / N
i = N+1, N+2, …
Examples
The chart below shows green icons when DMI+ crosses above DMI-, which generates a bullish signal. This means the DMI+ value is greater than the DMI- value for the first time. The red icon (bearish signal) is generated when DMI- crosses above DMI+. The results look at the signals in isolation, entering into a position for Gold and holding it for an arbitrary number of days (the default is 20 days but can be adjusted from the amber box in the top-center). This is a great tool to get a quick pulse on performance without identifying a rules-based exit and can also be used to screen for signals across a list of names (leverage the launch menu on the red toolbar for this). One way you can modify this strategy is by adding an additional condition that considers the ADX value. When the ADX is 25 or greater, this signifies a trending market, which can help eliminate signals during sideways moves.
BQL Example
=BQL("EUR Curncy", "dmi(close=px_last(), high=px_high(), low=px_low(), period=14).adx")
Return to Top
GM Calculations
The Money Flow (GM) function uses the following calculations.
Money Flow Calculation
Bloomberg's money flow analysis applies to stocks and selected stock indices. Index money flows are the sum of the money flows of the component stocks. Money flows are only calculated when the price of the security changes and include only those trades from the security's primary exchange.
The value of money flow is set to zero at the start of the trading day. When a trade is performed, its price is compared to the price of the previous trade (the first trade of the day is compared to the previous day's close). If the prices differ, the money associated with the trade (price times number of shares) is added to or subtracted from the money flow. Additions (inflows, buys) are done on upticks; subtractions (outflows, sells) are done on downticks.
Historical money flows are calculated with the zero point at the close of the day prior to the first trading day under review (rather than at the start of each trading day). The effect is that of a continuous stream of trades from the open of the first day under review to the close of the last day under review. Therefore, historical money flows are dependent on the start date.
Money Flow Calculation Interpretation
In general, money flow trends confirm price trends. As prices rise, money flows are usually positive. As prices fall, money flows are usually negative. A divergence, however, between money flow and price trend can be a signal of a future price trend change. For example, a falling stock price with a positive money flow can indicate a future rally in the price of the stock.
Money Flow for US Equities
US money flow calculations use the US Composite tick stream to calculate the value. This provides a more accurate and reliable value which measures the net money moving in to or out of a stock. Historically, money flow for US equities defaulted to primary exchange data only.
For Stock Indices, for example, SPX <INDEX>, money flow will continue to use the local exchange of its members, e.g. UN, UW, etc., in the calculation.
Return to Top
EFMF Calculations
The Estimated Fund Money Flow (EFMF) function fund flow is calculated using the shares outstanding and fund NAV. The following table provides a simplified example of the calculation.
Estimated Money Flow (EMF) for Funds
Derived using the following formula:
ETF Net Fund Flow = [Shares Outstanding (t) - Shares Outstanding (t-1)] * NAV (t)
Non-ETF Net Fund Flow uses one of the below methods, depending on data availability:
If fund reports shares outstanding and NAV:
[Shares Outstanding (t) - Shares Outstanding (t-1)] * NAV (t)
If fund reports class assets and NAV:
[Derived Shares Outstanding (t) - Derived Shares Outstanding (t-1)] * NAV (t)
WhereEquals
Shares Outstanding (t)
Shares outstanding as of the end date of the period of the analysis.
Shares Outstanding (t - 1)
Shares outstanding as of the start date of the period of the analysis.
Derived Shares Outstanding (t)
Class Assets divided by Net Asset Value on end date of the period of the analysis.
Derived Shares Outstanding (t-1)
Class Assets divided by Net Asset Value on start date of the period of the analysis.
NAV (t)
Net Asset Value (NAV) of a mutual fund or exchange-traded fund (ETF) as of the start date of the period of the analysis.
Note: If shares outstanding data (actual or derived) is not as frequent as NAV data, average NAV is used for fund flow calculations. The flow is calculated at share class level, is not calculated for cross-listed tickers, and is not available for closed-end funds.
Return to Top
Interpreting an EFMF Study
The following is an example of an EFMF study and how it can be interpreted.
In the chart below, the fund price exhibits an upward trend until June 2007. After June, the fund price declines until March 2009, before moving upward again throughout the rest of the date range.Looking at the study panels under the main chart, you can see that the Cumulative Net Money Flow (in panel 3) remains positive throughout the decline from 2007-2009, before turning negative despite improved periods of fund performance.
In the example above, the AUM Period field (in the control area) is set to 1 by default. This means that on a monthly chart, monthly periodic changes are plotted while on a yearly chart, yearly periodic changes are plotted. From the control area, you can modify the AUM period field by entering a new value in the AUM Period field. For example, if you set the field to 6, on a monthly chart the semi-annual periodic changes are plotted.
You can enhance the usefulness of the study by adding the Fund Total Assets (AUM) field to the study as is done in the following chart.
The example above shows the AUM climbing until June 2006. You can see this is due to a combination of the Cumulative Net Money Flow (in panel 3) which shows the accumulated Periodic Net Estimated Money Flow Money (in panel 2) and the positive performance of Periodic Total Return ( in panel 4). After this the AUM drops off more steeply than price, despite periods of positive performance and cumulative net money flow remaining positive until July 2010.
Return to Top
Fear and Greed
Fear and Greed is an oscillator based on the Average True Range (daily high/low range, adjusted for gaps) to measure the ratio of buying strength to selling strength. This tells us whether the Bulls or the Bears are in control at a particular point in time. It is an excellent oscillator for divergence analysis and for identifying trend persistence.
To understand the Fear and Greed indicator, it is important to understand the concepts of True Range and Average True Range. True Range looks at the relationship between the current bars high and low, and compares it to yesterdays close to identify the largest range. For example, if the current high is $12 and the current low is $10 dollars, the range would be is $2. If yesterday's close was $9, today's True Range would be $3. True Range adjusts for gaps between the prior day's close and the current day's open to determine the True Range. Average True Range is a simple or exponential moving average of the True Range values historically.
The Fear and Greed indicator is the spread of two weighted moving averages of the True Range. It is calculated in a way that it oscillates on a zero base line.
Interpretation
A bullish signal is generated when Fear (red) turns to Greed (green) and a bearish signal is generated when Greed (green) turns to Fear (red). When fear or greed spikes to extreme levels it is signaling the start of a top or bottom . It's also possible to identify trends and trend exhaustion through divergence analysis. A sign of bullish divergence would be when price is trending lower and fear is reaching higher lows. A sign of bearish divergence would be when price is trending higher and greed is hitting lower highs. Both of these could indicate signs of an exhausted trend.
It's also important to understand how to interpret the legend. As shown in the image below, the indicator displays FG(5.00), which represents the sensitivity factor. Depending on your investment style, increasing or decreasing the value of this will speed up or slow down the rate of change of the Fear and Greed value.
Calculations
The core calculation uses an On Balance aggregation of TrueRange, as discussed above in the description, with True range being the greatest of the following:
Today's high minus today's low
The absolute value of today's high minus yesterday's close
The absolute value of today's low minus yesterday's close
On an up close the TrueRange is added and on a down close the TrueRange is subtracted.
Thereafter, a Weighted Moving Average of period "First LookBack" is applied followed with a second Weighted Moving Average with a period determined by the "Look Back Period" value. If "Look Back Period" is not 0, then it is used directly. If "Look Back Period" is 0, the second period used is the rounded value of the Sensitivity squared. The final oscillator output is the difference between the averaged lines.
BQL Example
=BQL("EUR Curncy", "radar1FG()")
Return to Top
Fisher Transform
Fisher Transform is a technical indicator that converts prices into a Gaussian normal distribution. Sharp turning points in the indicator happen where the rate of change is the largest and clearly identify price reversals in a timely manner.
Market prices do not have a Gaussian probability density function or the familiar bell-shaped curve of a normal distribution. The distribution of returns tends to be symmetrical around their means, but the tails are fatter than expected because there are more outliers. The fat tails can make charts noisy and difficult to interpret for market technicians.
Fisher Transform creates a nearly Gaussian probability density function by normalizing prices. The transformation makes peak swings relatively rare events and unambiguously identifies price reversals on a chart. The indicator is commonly used by traders looking for leading signals rather than lagging indicators.
Signals
Fisher Transform above 2 or below -2 can be interpreted like a Z Score: as an extreme deviation from the trend, thus possibly overbought or oversold.
Fisher Transform crossing its own moving average can indicate a shift in momentum.
Divergences between peaks and troughs of the price versus peaks and troughs of the indicator can signal a change in trend.
Example
In the chart of DAX below:
The red arrows highlight a bearish divergence.
The green vertical line marks a mean reversion point as the Fisher turns back upwards from beneath -2.
Calculations
Inputs: Price((H+L)/2), Len(5);
Vars: MaxH(0), MinL(0), Fish(0);
MaxH = Highest(Price, Len); MinL = Lowest(Price, Len);
Value1 = .33*2*((Price - MinL)/(MaxH - MinL) - .5) + .67*Value1[1];
If Value1 > .99 then Value1 = .999; If Value1 < -.99 then Value1 = -.999;
Fish = .5*Log((1 + Value1)/(1 - Value1)) + .5*Fish[1];
BQL Example
=BQL("DAX Index", "fshtr(close=px_last(), high=px_high(), low=px_low(), period=5, ma_type=SIMPLE, ma_period=20)")
Return to Top
Hurst Exponent
The Hurst Exponent is a technical indicator that uses historical information to predict future prices, assuming that prices persist or reverse direction more often than they are random. It is also known as the index of dependence.
Interpretation
When a time-series is random, H = 0.5. When H is greater than 0.5, the time series is persistent, while if it is less than 0.5 it is anti-persistent. If a time series' H = 0.7, then the time series has a greater probability of continuing its current direction and a lesser probability of reversing itself. The converse is true for an anti-persistent time series.
Example
A period of trend consistency in the S&P 500 produces a higher Hurst value (green rectangle) whereas a period of unpredictability results in a value closer to 0.5 (red rectangle).
Calculation
X(t) = 1/aH X(at)
Where:
X(t) is a function in time 1/aH is the scaling factor X(at) is the process X(t) accelerated up by a factor of "a".
When a time-series is random, H = 0.5. When H is greater than 0.5, the time series is persistent, while if it is less than 0.5 it is anti-persistent. If a time series' H = 0.7, then the time series has a greater probability of continuing its current direction and a lesser probability of reversing itself. The converse is true for an anti-persistent time series.
BQL Example
=BQL("EUR Curncy", "atr(close=px_last(), period=5)")
Return to Top
Ichimoku
The Ichimoku study was developed by Goichi Hosoda in the late 1930s and published in the 1960s. Ichimoku may be referred to as "Ichimoku Cloud" or "Ichimoko Kinko Hyo" (one look equilibrium chart) as well. The study consists of five lines (see the Calculation Details list below) which are used to define trend direction as well as support and resistance levels. The Leading Span 1 (or Senkou Span A) and Leading Span 2 (or Senkou Span B) combine to form the cloud.
Calculation Details
Conversion Line (or Tenka-sen line): Calculated on a nine-period basis by summing the highest price and the lowest price for the period, and dividing the result by 2.
Base Line (Kijun-sen line): Calculated on 26-period basis by summing the highest price and the lowest price for the period, and dividing the result by 2.
Lag Line (or Chikou Span or Lagging Span): Close price, lagged or shifted left by lag period (26 days)-1. Given day X, this is the price as of the lag period-1 (25 days) ahead.
Leading Span 1 (or Senkou Span A): (Conversion line + Base Line)/2, shifted right by lead period (26 days)-1. Given day X, the two lines are summed and divided by 2, as of 25 days prior to X.
Leading Span 2 (or Senkou Span B): The highest closing price over 2* lead period (26 days, 52 in total) + lowest closing price over 2* lead period (26 days, 52 in total))/2 shifted right by lead period (26 days)-1. This means, given day x, the leading span 2 will be the value from 25 days prior, calculated on 52 periods as detailed above.
Signals
There are several signals in the Ichimoku study. Some of the most common signals are:
Price and Lag lines are above the cloud (bullish bias)
Conversion line crosses above the Base line (bullish)
Price and Lag lines are below the cloud (bearish bias)
Conversion line crosses below the Base line (bearish)
Example
As shown in the image below, after finding support at the cloud multiple times, the Dollar Index price finally broke below in mid 2020. The price then found resistance at the cloud, as highlighted by the yellow circle. The subsequent break below the cloud of the Lag Line, as indicated by the yellow arrow, marked the start of a new bear trend.
Return to Top
MACD (Moving Average Convergence/Divergence)
Moving Average Convergence/Divergence (MACD) is a trend-following momentum indicator that expresses the relationship between two exponential moving averages (EMAs) of a security's price. MACD, developed by Gerald Appel, shows characteristics of both a trending indicator and an oscillator. While the primary function is to identify turning points in a trend, the level at which the signals occur determines the strength of the reading.
MACD is calculated by subtracting one "slow" EMA from a "fast" EMA. (The slow EMA is calculated over a longer time period than the fast EMA.) An EMA of the MACD, called the signal line, is then plotted on top of the MACD line. It functions as a trigger for buy and sell signals. Traders may buy the security when the MACD crosses above its signal line and sell/short the security when the MACD crosses below the signal line.
The MACD has a positive value when the fast EMA is above the slow EMA, and a negative value when the fast EMA is below the slow EMA. The more distant the MACD is above or below its baseline, the more distant the two EMAs are growing.
Signals
The three most popular ways to use the MACD are Crossovers, Divergences and Overbought/Oversold conditions.
Crossover: The basic MACD trading rule is to sell when the MACD falls below its signal line, and to buy when the MACD rises above its signal line.
Divergences: Indicates that an end to the current trend may be near, and occurs when the MACD diverges from the security. A divergence occurs when the trend of a security's price doesn't agree with the trend of the MACD. A bearish divergence occurs when the MACD is making new lows while prices fail to reach new lows. A bullish divergence occurs when the MACD is making new highs while prices fail to reach new highs. When this occurs, prices usually change direction to confirm the trend of the MACD.
Overbought/Oversold Conditions: When the shorter moving average pulls away dramatically from the longer moving average (i.e., the MACD rises), it is likely that the security price is overextending and will soon return to more realistic levels.
MACD2 (line or histogram) MACD2 is another indicator value that can be viewed on the chart either as a line or a histogram. MACD2 shows the difference between the MACD and the signal. High MACD2 values are seen when trends are moving strongly in one direction, either up or down. Falling and low MACD2 values are evidence of a weakening trend and possible crossovers. A popular use of MACD2 is as an "early-warning" strategy that entails closing out the current position when the MACD2 value begins the fall from its extreme point, instead of waiting for the reverse crossover to occur.
Example
MACD plots the spread between a 12- and 26-period moving average, and is displayed in white. A 9-day EMA of the MACD, called the "signal" line, is plotted on top of the MACD in red. Because the MACD is considered a trend-following indicator, it proves most effective in wide-swinging or trending markets. MACD and moving averages are both examples of trend following, or "lagging" indicators.
Calculations
MACD Line: MACD=Period1 Exponential MA (Fast) -Period2 Exponential MA (Slow)
MACD Signal Line: Sig=Period3 Exponential MA of MACD Line
MACD Diff: Diff=MACD - Sig
Where:
Period1 = N Period of the Fast Exponential MA (the default Period1 is 12)
Period2 = N Period of the Slow Exponential MA (the default Period2 is 26)
Period3 = N Period Exponential MA for the Signal Line (the default Period3 is 9)
MACD Period: N Period = For daily, N=days; weekly, N=weeks, ...
MACD omits non-trading days from computations.
Non-trading days are omitted from the calculation.
BQL Example
=BQL("AAPL US Equity", "macd(close=px_last(), period1=12, period2=26, period3=9)")
Return to Top
MAE (Moving Average - Envelopes)
Moving Average - Envelopes (MAE) is a type of moving average that lets you gauge a security's trading activity and identify price trends by plotting percentage-based support and resistance levels for a selected security along with a simple moving average. The support and resistance levels form a moving average "envelope."
MAE defaults to 3% percentage bands and a 15-day moving average. The optimum percentage shift depends the volatility of the security -- the more volatile, the larger the percentage shifts should be. The theory behind envelopes is that overzealous buyers and sellers push prices to extremes, i.e. the upper and lower bands, at which point prices often stabilize by moving to mean reversion levels.
When the price of a security reaches the top band, it is assumed that resistance will be encountered; at this point a signal to sell is implied. When the price of a security reaches the lower band, the assumption is support will be found; at this point the signal to buy is implied. In situations where the price action breaks through the top or bottom band, a breakout has occurred and the continuation of the current trend is expected.
To display an MAE chart, enter GPO MAENV <GO>.
BQL Example
=BQL("AAPL US Equity", "mae(close=px_last(), period=5, upper_band=2, lower_band=2)")
Return to Top
MDI (McGinley Dynamic Indicator)
McGinley Dynamic Indicator is a technical indicator that improves on the moving average (MA) by removing one of its major flaws: its inability to speed up/slow down automatically when the underlying price does. The normal MA's length is fixed and does not change dynamically. As a result, in a fast market, the MA is often left far behind (i.e., the gap between price and the MA is often so large as to render the MA useless), because a faster MA is suddenly required.
The McGinley Dynamic Indicator (MDI), developed by John R. McGinley, solves this problem by automatically adjusting the speed of the MA when the price changes speed (both up and down). Additionally, since down markets are generally more explosive and faster than up markets, the MDI adjusts more rapidly in down markets than in up.
Signals
Like a moving average, price crossing the McGinley line can signal changes in trend.
Changes in the slope of the line can also represent shifts in trend direction.
Example
In the chart below, the S&P 500 is blue when the close price is greater than the McGinley line and red when it is below.
Calculations
MD = MD1 + (Price - MD1) / (N * (Price / MD1) ^ 4), where:
MD1 refers to the prior value of the Dynamic Indicator
N refers to a Dynamic Tracking Factor
Non-trading days are omitted from the calculation.
BQL Example
=BQL("SPX Index", "mcgdi(close=px_last(), ma_period=14, ma_type=EXPONENTIAL, factor=125, offset=1)")
Return to Top
MLR (Moving Linear Regression)
Moving Linear Regression is a technical indicator that fits an unseen line to a rolling set of data points using the "least squares" technique. This technique finds the line that minimizes the sum of the squares of the distances between each point and the line, and the value of the last point (i.e., the end point of the fitted line) is returned.
It also returns upper and lower bands around the Moving Linear Regression.
Signals
MLR can be used to define trend direction either by the slope of the line or by the price crossing the line.
A break above or below the bands may indicate a breakout a new trend or volatile move (see chart below).
Alternatively the upper and lower bands can be used as mean reversion points.
Example
The chart below shows how breaks above and below the bands characterized strong bursts into a new trend.
BQL Example
=BQL("SPX Index", "mlr(close=px_last(), offset=5, period=14, extension=0, band_type=STDERR, upper_band=1, lower_band=1)")
Return to Top
MLRR (Moving Linear Regression - R-Squared)
Moving Linear Regression - R-Squared is a technical indicator that measures the strength of a trend. It begins by fitting an unseen line to a rolling set of data points using the "least squares" technique. This technique finds the line that minimizes the sum of the squares of the distances between each point and the line. The indicator then calculates the linear regression r-squared of the fitted line at each point.
MLR R-Squared also returns a moving average of the R-squared of the Moving Linear Regression.
To display an MLR R-Squared chart, enter GPO MLRR <GO>.
Signals
MLR R-Squared does not give directional signals, but instead indicates the strength and consistency of a trend.
A reading above a certain level could be used in conjunction with a trend following indicator to identify an entry point in a trend following strategy.
Conversely, a reading below a certain level could be used to define a range-bound market in which an oscillator study could be used to identify entry points for a mean reversion strategy.
MLR R-Squared crossing its moving average can be used to identify changes in trend regime.
Example
The highlighted areas on the chart below show how periods of relative trend consistency were characterized by high readings on the MLR R-Squared indicator.
BQL Example
=BQL("SPX Index", "MLRR(close=px_last(), ma_period=5, offset=0, ma_type=SIMPLE, period=14)")
Return to Top
MLRS (Moving Linear Regression - Slope)
Moving Linear Regression - Slope (MLRS) is a technical indicator that measures the magnitude of a trend. It begins by fitting an unseen line to a rolling set of data points using the "least squares" technique, which finds the line that minimizes the sum of the squares of the distances between each point and the line. The indicator then calculates the value of the slope of the fitted line at each point.
MLRS also returns a moving average of the slope of the Moving Linear Regression.
Signals
MLRS can be used to define trend direction based on whether its value is greater than or less than 0.
Changes in trend direction can be signaled by the MLRS crossing its moving average.
The peaks and troughs or the MLRS can be compared with those of the price to identify momentum divergences.
Example
The image below from BT <GO> shows the performance of a strategy based on going long the S&P 500 when its 52-week MLRS is positive and exiting when it turns negative.
Calculations
Where:
BQL Example
=BQL("XAU Curncy", "mlrs(close=px_last(), ma_period=5, offset=0, ma_type=SIMPLE, period=14)")
Return to Top
MOM (Momentum)
Momentum is a technical indicator that measures the net difference in price between two points on a chart. It is a trend-following, forecasting study based on behavioral finance and fractal geometry. The study is designed to support professional traders in their decision making process for any type of asset or exchange-based security. The study accuracy is well above 80% for any type of securities/markets or timeframes.
The momentum line is the difference between the closing price and the closing price N periods ago. A simple moving average (SMA) of the momentum line is also calculated. A buy signal is generated when the momentum line crosses above the SMA, while a sell signal is generated when the momentum line crosses below the SMA.
To display a Momentum chart, enter GPO MOM <GO>.
Interpretation
A buy signal is generated when the Momentum line crosses above the moving average. A sell signal is generated when the Momentum line crosses below the moving average line. The Momentum line is the difference between the closing price and the closing price N (typically 10) periods ago.
BQL Example
=BQL("SPX Index", "momentum(close=px_last(), period=10, ma_period=10)")
Return to Top
Psychological Line
The Psychological Line is a simple market sentiment index that measures the number of positive days out of a specified number of days. This result is multiplied by 100 to give a simple percentage scale for reference.
The indicator is generally applied as a measure of the positive closes over a period of 12 days, with a reading over 75 considered overbought and bearish and a reading under 25 considered oversold and bullish.
This indicator is an oscillator and is generally applied as a measure of the positive closes over a period of 12 days with a reading over 75 considered overbought and bearish, and a reading under 25 considered oversold and bullish. Moving from an oversold or overbought condition back into neutral territory can generate buy and sell signals respectively. This study can also be used as a divergence tool. Divergence occurs when price and the indicator move in opposite directions. Bullish divergence is when price is moving lower but the indicator moves higher, indicating a potential buying opportunity. Bearish divergence is when the price is moving higher but the psychological line is moving lower, signaling a potential sell opportunity. As an oscillator, this indicator is often paired with a trending study, like a moving average, to confirm the trend or change in trend.
Calculations
PSYCL = (Number of rising days in the past N period / Total number of days in N period) * 100
Where N is the number of bars used for the lookback period. The default is to 12 but can be customized.
Non-trading days are omitted from the calculation.
Example
To load a sample Psychological Line chart like the one below, enter TSIG <GO>. Then, click the Sample Signals sub-tab, and select Psychological Line from the list below.
The strategy is set up to display a green icon (buy) when the psychological line crosses above 25, and a red icon (sell) when the indicator crosses below a value of 75. As shown in the chart below, the statistics on the right show an entry into the US 10 Year rate on the day of the icon with an arbitrary holding period of 20 days, which can be modified via the box in the top-center. Considering the data over a two-year range, there is an average 3.44% gain.
BQL Example
=BQL("EUR Curncy", "psycl(close=px_last(), period=12)")
Return to Top
PTPS (Parabolic Studies)
Parabolic Studies is a technical indicator that shows stop-and-reversal (SAR) trading points for a given security. Developed by J Wells Wilde, the indicator aims to determine the direction an asset is moving. The SAR points are a function of price movement and time. They follow price using an acceleration factor (AF) that increases with the velocity of price movement. A break of the SAR points suggests closing the current position and entering a position in the opposite direction.
The indicators plots above price in a downtrend and below price in an uptrend. The indicator is not as reliable in a flat or range-bound market, so it may be paired with other indicators that identify trend strength for better signals. As it aims to identify potential reversals, a break of the SAR points suggests closing the current position and entering a position in the opposite direction. The signals can also be used to set stop losses and profit targets.
To display a Parabolic chart, enter GPO PTPS <GO>.
Calculations
Uptrend Parabolic Sar = Prior SAR + Prior AF(Prior EP - Prior SAR)
Downtrend Parabolic SAR = Prior SAR - Prior AF(Prior SAR-Prior EP)
EP is the extreme point in a trend. It is the highest price reached during an uptrend or the lowest price point reached during a downward move.
The acceleration factor (AF) defaults to a value of 0.02. It then increases by .02 each time the EP is recorded, with a max value of 0.20. This can be adjusted depending on trading style.
Non-trading days are omitted from the calculation.
Example
To load a sample Parabolic chart like the one below, enter BT <GO>. Then, from the Sample Strategies sub-tab, select Parabolic (PTPS).
In this sample backtest, the Parabolic Strategy goes long when price crosses above the Parabolic price level and short when the price crosses below Parabolic price level. The strategy is a reversal strategy through the use of the 'Cover and go Long' and 'Close and go Short' Actions, so it is always in the market. The Parabolic study properties of 'AF Factor', 'Maximum', and 'Start' can be changed for testing purposes using the available PTPS1 'Factor.' The results are based on 100k initial capital, where the entire pool of funds are put into each hypothetical trade that are signaled on the chart by the green (long) and red (short) arrows.
BQL Example
=BQL("EUR Curncy", "ptps(high=px_high(), low=px_low())")
Return to Top
RMI (Relative Momentum Index)
The Relative Momentum Index (RMI) is a technical indicator that is similar to the Relative Strength Index (RSI) in that it measures the velocity of a security's price movement to identify overbought and oversold conditions. However, it does not count up and down days from close to close. Instead, it counts up and down days from the close relative to a close N days ago. It is ultimately the ratio of the average upward changes to the average downward changes, over a given period of bars.
The indicator moves in the range of 0-100, with values above 70 and values below 30 considered as an indication of overbought and oversold conditions respectively. A high RMI level can often be an indicator of a positive price trend that can persist for many months. Further, an exponential moving average (EMA) is applied to the RMI and is used as a signal line. In this case, the RMI indicator consists of two lines: the RMI line itself and the Signal line (EMA applied to the RMI).
Signals
A buy signal is generated when RMI values advance above 30 from below and when there is a crossover of the RMI and its signal line from below.
A sell signal is generated when RMI values drop below 70 from above and when there is a crossover of the RMI and its signal line from above.
Since RMI readings above 50 are considered as bullish and RMI readings below 50 are considered as bearish, some traders may choose to generate signals on the crossovers of the RMI and 50 center line: sell when RMI decline below 50 and buy when RMI advances above 50. Divergence between RMI and price direction is also taken into consideration by many traders as an indication of the possibility of a reversal in the near future.
Calculations
RMI = RM / 1+ RM
RM = average up moves (over N periods) / average down moves (over n periods)
Example
To display an RMI chart, enter GPC RMI <GO>.
BQL Example
=BQL("EUR Curncy", "rmi(close=px_last(), period=14, mom_period=10, ma_type=SIMPLE, ma_period=14)")
Return to Top
RSI (Relative Strength Index)
The Relative Strength Index (RSI) , developed by J. Welles Wilder, is a technical indicator that measures the velocity of a security's price movement to help identify overbought and oversold conditions. RSI helps you make entry/exit decisions by indicating potential turning points.
An RSI that falls below 30 indicates an oversold condition and a buy signal is usually triggered when the indicator crosses 30 from below. Similarly, an RSI greater than 70 indicates an overbought condition and a sell signal is usually triggered when the indicator crosses 70 from above. Divergences between the price action and the RSI can also imply reversals. Bearish divergence occurs when RSI make lower highs while price makes higher highs. A bullish divergence occurs when RSI makes higher lows while price makes lower lows.
To display an RSI chart, enter GPO RSI <GO>.
Calculations
RSI = 100 - [ 100 / (1 + [Avg Up/Avg Dn]) ]
Where:
Avg Up = N Period Smoothed MA of Up Closes;
Initial Avg Up = Simple MA of 1st N Up Closes;
Next Avg Up = ((Previous Avg Up * (N - 1)) + Today's Up Close) / N
Avg Dn = N Period Smoothed MA of Down Closes;
Initial Avg Dn = Simple MA of 1st N Down Closes;
Next Avg Dn = ((Previous Avg Dn * (N - 1)) + Today's Down Close) / N
Up Close:
if Today's Close > Yesterday's Close,
then Up Close = Today's - Yesterday's Close
else Up Close = 0
Down Close:
if Today's Close < Yesterday's Close,
then Down Close = Yesterday's - Today's Close
else Down Close = 0
N Period = For daily, N=days; weekly, N=weeks, ...
The default is 14
Example
To load a sample RSI chart like the one below, enter BT <GO>. Then, from the Sample Strategies sub-tab, select RSI. You can customize the ticker, date range, and periodicity for your own analysis.
A green icon (hypothetical buy) appears on the chart when the RSI line in the lower panel crosses above 30 from below. It stays long until a red icon appears (hypothetical short), which is triggered when the RSI line crosses below 70 from above. The far right-hand side of the screen shows that over this one-year time period, a total of four trades have occurred – two long and two short. Both long signals were profitable, while one short was profitable and the other short lost money. Overall, the strategy is still a winner, producing 125% return. To edit rules or modify assumptions around trade entry, click the Review button on the red toolbar.
BQL Example
=BQL("EUR Curncy", "rsi(close=px_last(), period=14, per=D)")
Return to Top
ROC (Rate of Change)
Rate of Change (ROC) determines the momentum behind price movements. It measures it either as percent change or price difference. When displayed as a percent the value shown means XX%. By running ROC <GO> you can chart the rates of price change for a selected security for up to four different time periods at once.
Price and ROC generally move in tandem. When price and ROC diverge, look for the rate of change to be the clearer indication of the underlying price trend. Another way to determine a buy signal is when there are continuous M number of positive ROC's, meaning the price has being going up every bar for the past M periods. A sell signal would be the reverse. Still, another way to consider a signal using ROC might be when price does an extreme rise or fall, this may indicate price is overextended and swing the other way.
To display an ROC chart, enter GPO ROC <GO>.
Example
To load a sample Rate of Change chart like the one below, enter TSIG <GO>. Then, click the Sample Signals sub-tab, and select 10% Weekly Drop from the list below.
The chart defaults to a weekly periodicity. A signal (icon) appears on the chart each time the one-week price change in is -10% or greater. When the signal occurs, the statistics on the right show that the average outcome of price movement over the following 12 weeks is a price appreciation of 21.5%. You can modify the holding period by changing the value (e.g., 12) above the chart area.
Calculations
ROC = (Current Price - Price N periods ago ) / Price N periods ago
For daily, N=days; weekly, N=weeks, ...
BQL Example
=BQL("EUR Curncy", "roc(close=px_last(), period=3, per=D, percent=TRUE)")
Return to Top
SMA (Simple Moving Average)
Simple Moving Average (SMA) is a type of moving average that is calculated by summing the closing price of the security over a period, then dividing by the length of the period. The moving average smooths the short-term fluctuations in the stock prices and allows us to identify a clear market trend. It is also known as SMA or the "arithmetic moving average."
Interpretation
A simple moving average is used as a stock's support and resistance level. When a moving average is below the stock's current market price, it can be used as a support level. When the moving average is above the stock's current market price, it can be used as a resistance level.
The crossover of two moving averages-like twenty-day and fifty-day moving averages-is used by some traders as entry and exit points. When the twenty-day SMA crosses over the fifty-day SMA, it's used as an entry signal. When the fifty-day SMA crosses over the twenty-day SMA, it's used as an exit signal in an uptrend and vice versa in a downtrend.
To display an SMA chart like the one below, enter GPO SMA <GO>.
Calculations
A simple, or arithmetic, moving average is calculated by adding the closing price of the security for a number of time periods (window lengths) then dividing this total by the number of time periods. For example, a simple moving average of a 20 day window is calculated as:
SMAVG(20) = [price(1) + price(2) + ... + price(20)] / 20.0
Non-trading days are omitted from the calculation.
BQL Example
=BQL("AAPL US Equity", "dropna(smavg(period=20, dates=range(-1Y, 0D)))"
Return to Top
Smoothed Moving Average
Smoothed Moving Average is one member of the Moving Average Indicators family, which tries to smooth the noise and show trends more clearly by taking all historical data into account. Unlike the Simple Moving Average indicator, which only uses fixed N data points into the each calculation, Smoothed Moving Average incorporates all historical data, which, as a whole, holds an equal weighting to the recent price; but, the older the overall data, the lower the weight. In this way, Smoothed Moving Average removes short-term fluctuation and helps to visualize the prevailing trend.
Signals
A buy signal is usually triggered when a shorter term moving average crosses from below to above a longer term moving average.
A sell signal is usually triggered when a shorter term moving average crosses from above to below a longer term moving average.
Alternatively current price can be compared to smoothed moving average, buy if price is above and sell if price is below the smoothed moving average.
Calculations
The first value of this smoothed moving average is calculated as the simple moving average:
(SMA): SUM1 = SUM (CLOSE (i), N) SMMA1 = SUM1 / N
The second moving average is calculated according to this formula:
SMMA (i) = (SMMA1*(N-1) + CLOSE (i)) / N Succeeding moving averages are calculated according to the below formula: PREVSUM = SMMA (i - 1) * N SMMA (i) = (PREVSUM - SMMA (i - 1) + CLOSE (i)) / N
Where: SUM - sum;
SUM1 - total sum of closing prices for N periods; it is counted from the previous bar;
PREVSUM - smoothed sum of the previous bar;
SMMA (i-1) - smoothed moving average of the previous bar;
SMMA (i) - smoothed moving average of the current bar (except for the first one);
CLOSE (i) - current close price;
N - smoothing period.
After arithmetic conversions the formula can be simplified:
SMMA (i) = (SMMA (i - 1) * (N - 1) + CLOSE (i)) / N
BQL Example
=BQL("AAPL US Equity", "ma(ma_type=SMOOTHED)")
Return to Top
Spearman Indicator
Spearman Indicator is an oscillator designed to determine overbought and oversold conditions in the markets. Developed in the early 1900s, it is also known as the "Spearman Coefficient." It is derived from an analysis of the correlation between a sorted list of prices and the original sequence of the prices. When the oscillator crosses above zero from below, it can be interpreted as a buy signal; crosses from above to below zero can be interpreted as sell signals.
Signals
When the oscillator crosses above zero from below it may be interpreted as a buy signal; crosses from above to below zero may be interpreted as a sell signal.
Calculations
Spearman Indicator is the so-called Spearman Rank Correlation Coefficient or Spearman's ρ. There are two methods to calculate Spearman's correlation depending on whether: (1) your data does not have tied ranks, or (2) your data has tied ranks. The formula for when there are no tied ranks is:
Where:
di = difference in paired ranks
n = number of cases.
The formula to use when there are tied ranks is:
Where:
i = paired score.
BQL Example
=BQL("VOD LN Equity", "dropna(sprmn(close=px_last(), dates=range(2020-08-01, 2020-08-14), ma_period=3, ma_type=SIMPLE, per=D, period=10))")
Return to Top
Stochastics
The Stochastic Oscillator measures the velocity of a security's price movement to identify overbought and oversold conditions. Developed by George C. Lane in the late 1950s with the belief that momentum changes direction before price, the indicator measures current price relative to highs and lows over a time period. In an up trend, markets tend to close near the high and while in a down trend they to close nearer to the lows. Stochastics can be used to recognize potential turning points to help make entry/exit decisions.
Traditional settings use 80 as the overbought threshold and 20 as the oversold threshold. Readings above 80 for the Stochastic Oscillator would indicate that the underlying security was trading near the top of its day high-low range over the set lookback period (e.g., 10 days). Readings below 20 occur when a security is trading at the low end of its high-low range. A break through these thresholds can be considered a first warning, but really it explains the current momentum of prices for the underlying security. There are traditionally two components displayed together in a given study panel - for instance, the %K and %D line. An example of a traditional bullish signal emerges when the faster line (%K) crosses above the slower line (%D) while in oversold territory. Some users see a confirmation of the bull signal when the %K line also crosses back into neutral territory. Conversely, a bearish signal emerges when the faster line crosses below the slower line while in overbought territory, with confirmation of the bearish signal given when the faster line can no longer remain overbought and crosses back below the threshold into neutral territory.
In addition to generating bullish and bearish signals with these traditional threshold, users often look for patterns of divergence. A bullish divergence forms when price records a lower low, but the Stochastic Oscillator forms a higher low. A bearish divergence forms when price records a higher high, but the Stochastic Oscillator forms a lower high.
Example
To load a sample Stochastic Oscillator chart like the one below, enter TSIG <GO>. Then, click the Sample Signals sub-tab, and select Stochastic Bullish from the list below.
The sample strategy is set up to give a green icon (hypothetical buy) when the Slow %K line crosses above the Slow %D line AND the slow %K line is less than a value of 20.
The statistics on the right side are based on an entry into the loaded security - AAPL Equity - on the day of the green icon with an arbitrary holding period of 20 days, which can be modified via the box in the top center showing "20." Considering the data over a 6 year time frame (top left under the loaded security), there is an average 4.58% appreciation in the price of Apple over that holding period, with 7 out of 8 signals showing an expected price rise.
Calculations
The Stochastics indicator has been interpreted in multiple ways by users over time. The Stochastics Fast/Slow study exposes additional methods of calculation to allow users a choice of any of the alternative interpretations. The Slow Stochastics study adds an additional smoothing step to the Fast Stochastics Fast %D calculation.
One parameter is the choice of the type of Moving Average type used. Stochastics Fast/Slow defaults to Smoothed Moving Average, while the traditional Stochastics indicator uses a Simple Moving Average. Additionally, Stochastics Fast/Slow includes the algorithm "Ratio of Moving Averages" that can be used as an alternative to the default algorithm "Moving Average of the Ratio".
Stochastics (TAS <GO>)Stochastics FastStochastics Slow
%K = 100*Closing Range/Total Range
Where:
Closing Range = Close - Range Minimum
Total Range = Range Maximum - Range Minimum
Fast %K = %K in Stochastic
%D = N-period Simple Moving Average of %K
Fast %D = N-period Smoothed Moving Average(Fast %K)
Algorithm 1: Moving Average of the Ratio
Fast %D = Moving Average(Closing Range/Total Range)
Algorithm 2: Ratio of Moving Averages
Fast %D = Moving Average(Closing Range) / Moving Average(Total Range)
Slow %K = Fast %D in Stochastics Fast
%DS = N-period Simple Moving Average of %D
Slow %D = N-period Smoothed Moving Average(Slow %K)
%DSS= N-period Simple Moving Average of %DS
BQL Example
=BQL("700 HK Equity", "tas(close=px_last(), high=px_high(), low=px_low(), period_k=14, period_d=3, period_ds=3, period_dss=3)")
Return to Top
Triangular Moving Average
Triangular Moving Average is a type of moving average that shows the average price of a security over a specified number of data points, and places the majority of weight on the middle portion of the price series. It is a double-smoothed simple moving average (SMA).
The most important element used in calculating the moving average is a time period, which should be equal to the observed market cycle.
The Triangular moving average is a lagging indicator, and will always be behind the price.
To display an Triangular Moving Average chart, enter GPO TRIMA <GO>.
Signals
Triangular Moving Averages allow you to identify bullish and bearish signals along with price trends:
Price crosses above TMA = Bullish Signal
Price crosses below TMA = Bearish Signal
A strong bullish or bearish trend can be seen when the Triangular moving average is very close to the price.
When a price is increasing, the Triangular moving average usually stays down because of the influence of the historical data.
Example
To load a sample Triangular Moving Average chart like the one below, enter BT <GO>. Then, from the Sample Strategies sub-tab, select Triangular MA.
Calculations
Triangular Moving Averages place the majority of weight on the middle portion of the price series. They are double-smoothed simple moving averages calculated as:
X = (window length + 1) / 2
X_Round = Round(X); X_Trunc = Trunc(X).
A simple moving average is calculated using X_Trunc as the window length.
A simple moving average is then calculated again on the previous moving average using X_Round as the window length.
BQL Example
=BQL("AAPL US Equity", "tmavg(close=px_last(), period=10)")
Return to Top
Trender
The Bloomberg Trender Indicator is an adaptive indicator that defines the degree and direction of the trend in a way that attempts to capture the majority of the position profit while minimizing whipsaws. The tool is designed to stay just out of range of the typical pullbacks in price within the trend.
Note: The Bloomberg Trender calculation is proprietary. Non-trading days are omitted from the calculation.
The input value, "Sensitivity", adjusts the probability for the next day's expected range to stay within the limits projected by the Trender algorithm.
If the "Use Close" option is enabled, then the close must breach the trailing trender value before the trend is reversed. Otherwise the high and low are used to determine the trend reversal.
Signals
Sell Signal: Close crosses below the TrendUp Line from the n-1 period. When switching from a TrendUp (green line) to TrendDown (red line) environment, a sell signal is triggered.
Buy Signal: Close crosses above the TrendDown Line from the n-1 period. When switching from a TrendDown (red line) to TrendUpd (green line) environment, a buy signal is triggered.
Example
To display a Bloomberg Trender chart like the one below, enter GPO TRNDR <GO>.
BQL Example
Trender Up Series: =BQL("EUR Curncy", "trender(close=px_last(), high=px_high(), low=px_low(), sensitivity=SHORTTERM3, use_close=1).trenderup")
Trender Down Series: =BQL("EUR Curncy", "trender(close=px_last(), high=px_high(), low=px_low(), sensitivity=SHORTTERM1, use_close=1).trenderdown")
Return to Top
Ultimate Oscillator
The Ultimate Oscillator is a technical indicator that uses the weighted average of three different time periods to reduce the volatility and false transaction signals that are associated with many other indicators that mainly rely on a single time period. Buy or sell "pressure" (i.e., where a security closes in relation to its true range) is determined over the three time periods (typically periods of 7, 14, and 28 bars), then combined using a 4:2:1 weighting.
Signals
There are three steps to a buy signal:
First, a bullish divergence forms between the indicator and security price. This means the Ultimate Oscillator forms a higher low as price forges a lower low. The higher low in the oscillator shows less downside momentum.
Second, the low of the bullish divergence should be below 30. This is to ensure that prices are somewhat oversold or at a relative extremity.
Third, the oscillator rises above the high of the bullish divergence.
There are three steps to a sell signal:
First, a bearish divergence forms between the indicator and security price. This means the Ultimate Oscillator forms a lower high as price forges a higher high. The lower high in the oscillator shows less upside momentum.
Second, the high of the bearish divergence should be above 70. This is to ensure that prices are somewhat overbought or at a relative extremity.
Third, the oscillator falls below the low of the bearish divergence to confirm a reversal.
Example
To display an Ultimate Oscillator chart like the one below, enter GPO ULTO <GO>.
Calculations
Buying Pressure (BP) = Close - Minimum (Low or Prior Close).
True Range (TR) = Maximum (High or Prior Close) - Minimum (Low or Prior Close)
Average7 = (7-period BP Sum) / (7-period TR Sum)
Average14 = (14-period BP Sum) / (14-period TR Sum)
Average28 = (28-period BP Sum) / (28-period TR Sum)
Ultimate Oscillator (UO) = 100 X [(4 x Average7) + (2 x Average14) + Average28] / (4+2+1)
Non-trading days are omitted from the calculation.
BQL Example
=BQL("EUR Curncy", "ulto(close=px_last(), high=px_high(), low=px_low)")
Return to Top
Variable Moving Average
Variable moving averages are exponential moving averages that automatically adjust the smoothing percentage based on the volatility of the data series - the more volatile the data series, the more weight given to values that are more recent. Different volatility ratios are used for variable moving averages.
Signals
If price crosses above the variable moving average, a buy signal is triggered (long position)
If price crosses below the variable moving average, a sell signal is triggered (short position)
Price can also bounce off the VARMA, which can act as levels of support and resistance
Example
To display a Variable Moving Average chart like the one below, enter GPO VARMA <GO>.
Calculations
NetChgSum = SUM[ABS(Close - (Close >> 1) ), Period
Max = Max[Close, Period]
Min = Min[Close, Period]
Quotient = (Max - Min)/NetChgSum
VR= Quotient / (Quotient >> 12)
VARMA = (VARMA >> 1) * (1-.078 * VR) + (.078 * Close)
Where:
.078 is the smoothing constant; VR = Volatility Ratio; ' Close >> 1 ' = Yesterday's Close Value
Non-trading days are omitted from the calculation.
BQL Example
=BQL("AAPL US Equity", "vmavg(close=px_last(), period=5, offset=0)")
Return to Top
Weighted Moving Average
A weighted moving average is designed to put more weight on recent data and less weight on past data. The weight of each price is based on the sequence of the price in the specific period.
Signals
If price crosses above the variable moving average, a buy signal is triggered (Long position)
If price crosses below the variable moving average, a sell signal is triggered (Short position)
Price can also bounce off the WGTMA, which can act as levels of support and resistance
Example
To display a Weighted Moving Average chart like the one below, enter GPO WGTMA <GO>.
Calculations
Lookback Period = n
WGTMA = C*n + (C>>1 * n-1) + (C>>2 * n-2).....) / (n + (n-1) + (n-2).....)
Non-trading days are omitted from the calculation.
BQL Example
=BQL("AAPL US Equity", "wmavg(close=px_last(), period=5, offset=0)")
Return to Top
WLPR (Williams %R)
Williams %R is an oscillator that measures the momentum of a security over a specified time period, based on the current price relative to highs and lows over that period. It can help you determine overbought/oversold levels and recognize potential turning points for making entry/exit decisions.
Signals
Overbought/Oversold: Traditional settings use 80 as the overbought threshold and 20 as the oversold threshold. Readings below -80 would indicate that the underlying security is trading near the bottom of its 14-period high-low range. Readings above -20 would indicate that the underlying security trading near the top of its 14-period high-low range.
Bullish/Bearish Divergence: The Williams %R scale, which oscillates between 0 and -100, is an inverse scale of Stochastics Fast. The center point of the scale, -50, is used as a general indicator of potential bullish and bearish biases within the market. A value for the given period that is greater than -50 is bullish and a value below -50 is bearish. A bullish divergence forms when price records a lower low, but the Stochastic Oscillator forms a higher low. A bearish divergence forms when price records a higher high, but the Stochastic Oscillator forms a lower high. For more: Stochastics.
Example
To display a Williams %R chart like the one below, enter WLPR <GO>. The default period for the indicator is 14 periods for all chart types (e.g., intraday, daily, weekly, monthly).
Calculations
WLPR = -100*(N Period Highest High - Close) / (N Period Highest High - N Period Lowest Low)
Where:
Highest High = The highest High over the specified N Period.
Lowest Low =The lowest Low over the specified N Period.
N Period = For daily, N=days; weekly, N=weeks, ...
The default is 14.
Non-trading days are omitted from the calculation.
BQL Example
=BQL("SPX Index", "wlpr(high=px_high(), low=px_low(), close=px_last(), period=14, per=D)", "fill=PREV")
Return to Top
Z-Score
Z-score is a technical indicator that measures the distance (in standard deviations) that a data series falls from its moving average. For example, a z-score of 2.37 indicates that a value is 2.37 standard deviations away from its moving average on the same date.
This indicator is based on the same theory as Bollinger Bands, but generates an alternative measurement that can then be interpreted and used to make determinations about market action.
Signals
If the z-score is outside a threshold of 2 standard deviations, it is likely the price will revert back to the average:
Bearish Signal: Z-score > 2
Bullish Signal: Z-score < -2
Example
To display a Z-score chart like the one below, enter GPO ZSCOR <GO>.
Calculations
Z Score = (X-M) / StdDev
X= Observed Value (close, open, low, high)
M = Average of the dataset
StdDev:
Non-trading days are omitted from the calculation.
BQL Example
=BQL("AAPL US Equity", "ta_zscore(close=px_last(), period=30, upper_band=2, lower_band=2)")
Return to Top

---
