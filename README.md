# Binary Return Note Valuation

The structure of a Binary Return Note is similar to the one of a regular note, but the coupons are
contingent on return rates on stocks. Quasi-Monte Carlo simulation is used for pricing the product. 

Let S1,…,Sn be n stocks (underlying prices) or stock indices. They can be in different currency markets. Let 0 be the current time and T be the maturity date. The following notation is used.

T1 , T2 ,…, T p  = T: reset date schedule;
K1  ,K2  ,...,K n : list of strikes;
PBR = POSITIVE _ BINARY _ RETURN : fixed positive constant;
N: the notional.

For each reset date T j,  j=1,…, p and stock price j , = 1,..., S i, ,i = 1,..., n , define return rates as:

 

At each reset date T j j=1,…, p coupons j , = 1,..., H j  j = 1,...p, are formed as follows:

 


where Fl j  are local floor and (w i ) i =1,...,n are positive weights that add up to 1. If
LAST_PERIOD_FLOORED_IND=NO, then Fl p  = 0 . The coupons are then paid at dates
T j j = 1,…, p , respectively. At maturity, T p = T  the notional is also paid.

The current value of a Binary Return Note with the new feature presented above can be written as

 

where is the discounting factor for time t as seen at current time 0. The above expectation is
in a world that is risk-neutral with respect to the payoff currency assuming deterministic interest
rates. As we may have underlying in different currency markets, we need to represent all dynamics in the payoff currency measure. Quasi Monte Carlo (QMC) method (Sobol low discrepancy sequences and Brownian bridge path generation. Such a method has an improved convergence speed. QA uses crude Monte Carlo for comparison.

With Monte Carlo approach, GAT calculates sensitivities as follows.

 

The spot exchange rate is denoted here by X. For the main issues that arise when computing sensitivities. It is known that Gamma requires a high number of simulations.

The three deals used differ by the stock correlation matrix (the last two of them are extreme cases), as this is one the most important risk factor (multi-path generation starts with a multi-dimensional Brownian motion whose correlation matrix is our stock correlation matrix).
In order to measure the difference, we use the following measure:

Considering the Monte Carlo nature of the model, the differences for Delta and Vega are reasonably small for all test cases. As expected we notice big relative differences in Gamma. This happens typically when the magnitude of Gamma is small. Middle Office should independently study Greek convergence. Gamma should be monitored too.

VALUATION_AS_OF_DATE 20050523
VALUATION_AS_OF_TIME 23:00
OUTPUT_DETAIL_LEVEL ALLMAX
OUTPUT_DETAIL_LEVEL PRINT_DECIMALS10
OUTPUT_DESTINATION stdout
GREEKS DELTA_VEGA_GAMMA //ALL
MC_HIDUM -111926486
MC_VARIANCE_REDUCTION SOBOL_SEQUENCE
//MC_VARIANCE_REDUCTION GAUSSIAN //SOBOL_SEQUENCE
MC_NSIMULATIONS 100000
MC_STEPDATE_FILE step_date_file.dat
MC_SIMULATION_END_DATE 20110523
MC_SIMULATION_END_TIME 19:00
RANDOM_OBJECT_TYPE EQUITY
UND_CURRENCY CAD=
UNDERLYING TSE35
EXCHANGE Z
DIVIDEND_YIELD 0.02
STD_FILE 0.15
ACTUAL_STOCK_PRICE 120
DRIFT_RATE_FILE /home/ts/rate_curve/CAD_RATE_CURVE.050520 (see https://finpricing.com/lib/IrCurve.html)
UND_CURRENCY_STRIP_RATE_FILE /home/ts/rate_curve/CAD_RATE_CURVE.050520
UND_CURRENCY_STRIP_DATE_FILE strip_date_file
RANDOM_OBJECT_TYPE EQUITY
UND_CURRENCY USD=
UNDERLYING SPX
EXCHANGE Z
DIVIDEND_YIELD 0.02
STD_FILE 0.15
ACTUAL_STOCK_PRICE 100
DRIFT_RATE_FILE /home/ts/rate_curve/USD_RATE_CURVE.050520
UND_CURRENCY_CORR -0.3
UND_CURRENCY_STD 0.05
UND_CURRENCY_EXCHANGE_RATE 1.515
UND_CURRENCY_STRIP_RATE_FILE /home/ts/rate_curve/USD_RATE_CURVE.050520
UND_CURRENCY_STRIP_DATE_FILE strip_date_file
RANDOM_OBJECT_TYPE EQUITY
