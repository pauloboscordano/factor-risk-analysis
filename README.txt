# Factor Risk Analysis: Understanding the Drivers of Portfolio Returns

A multi-factor analysis of systematic return and risk drivers across a diversified multi-asset universe using Python.

## Research Question

**What systematic factors explain the returns and risk of a diversified multi-asset portfolio, and how stable are those exposures over time?**

## Project Overview

Traditional portfolio analysis often focuses on total volatility and correlations between assets. However, portfolios that appear diversified across securities may still share common underlying sources of systematic risk.

This project analyzes the factor structure of eight ETFs representing equities, bonds, commodities, and international exposures over the 2015–2025 period.

The analysis combines static multi-factor regressions, rolling factor exposures, stress-period analysis, and portfolio-level factor risk attribution to identify not only how much risk is present, but where that risk comes from and how its underlying drivers evolve through time.

## Asset Universe

| Ticker | Exposure |
|---|---|
| SPY | U.S. large-cap equities |
| QQQ | U.S. technology-oriented equities |
| IWM | U.S. small-cap equities |
| ECH | Chilean equities |
| TLT | Long-term U.S. Treasury bonds |
| GLD | Gold |
| EMB | Emerging-market bonds |
| CPER | Copper |

## Systematic Factors

The baseline model includes five systematic financial factors:

- **MKT** — SPY return, representing broad equity-market conditions.
- **VIX** — Daily change in the CBOE Volatility Index, representing changes in financial uncertainty and risk aversion.
- **RATE** — Daily change in the U.S. 10-year Treasury yield.
- **USD** — Daily return of the U.S. Dollar Index.
- **COM** — Copper return, representing commodity and global cyclical conditions.

The baseline specification is:

**R(i,t) = α(i) + β(MKT,i)MKT(t) + β(VIX,i)ΔVIX(t) + β(RATE,i)ΔYIELD(t) + β(USD,i)USD(t) + β(COM,i)COM(t) + ε(i,t)**

The estimated relationships are interpreted as empirical systematic exposures rather than causal effects.

## Methodology

The project is organized around five complementary stages:

1. **Factor construction and exploratory analysis**
   - Daily asset returns and economically appropriate factor transformations.
   - Descriptive statistics, correlations, and multicollinearity diagnostics.

2. **Static factor estimation**
   - Multi-factor OLS regressions.
   - HC3 heteroskedasticity-robust standard errors.
   - Statistical significance and explanatory power.

3. **Dynamic factor exposure**
   - 252-trading-day rolling regressions.
   - Analysis of beta stability, magnitude, direction, and rolling R-squared.

4. **Stress-period analysis**
   - COVID-19 shock.
   - 2022 monetary-tightening episode.
   - 2025 market-uncertainty period.
   - Comparison of asset performance, factor behavior, and systematic risk composition.

5. **Portfolio factor risk attribution**
   - Equal-weight multi-asset portfolio.
   - Systematic variance decomposition using factor betas and the factor covariance matrix.
   - Rolling attribution of systematic risk through time.

## Standardized Factor Exposures

![Standardized Factor Exposures](figures/standardized_factor_exposures.png)

The standardized coefficients reveal economically distinct risk profiles across asset classes.

QQQ and IWM are primarily dominated by equity-market exposure, while TLT exhibits a strong negative interest-rate exposure. EMB combines market and interest-rate sensitivity, whereas ECH and GLD display broader combinations of market, currency, commodity, and uncertainty exposures.

## Explanatory Power of the Factor Model

![Factor Model Explanatory Power](figures/factor_model_explanatory_power.png)

The model explains approximately:

- **87.4%** of QQQ return variation.
- **80.1%** for TLT.
- **75.5%** for IWM.
- **55.2%** for EMB.
- **35.4%** for ECH.
- **26.9%** for GLD.

Systematic factors therefore have substantially different explanatory power across asset classes.

## Dynamic Factor Exposures

![Key Rolling Factor Exposures](figures/key_rolling_factor_exposures.png)

Rolling regressions show that factor exposures are not constant through time.

Several economically important relationships nevertheless remain highly persistent in direction:

- ECH maintains negative U.S. dollar exposure.
- EMB and TLT maintain negative interest-rate exposure.
- GLD maintains negative dollar exposure.
- IWM and QQQ maintain positive equity-market exposure.

The principal source of instability is often the **magnitude** of exposure rather than its direction.

## Time-Varying Explanatory Power

![Rolling Factor Model R2](figures/rolling_factor_model_r2.png)

The explanatory power of the factor model also changes over time.

QQQ remains strongly explained by systematic factors throughout most of the sample, while EMB and particularly ECH exhibit considerably greater variation in rolling R-squared.

This indicates that the importance of systematic versus idiosyncratic drivers is itself time-varying.

## Portfolio-Level Factor Model

An equal-weight portfolio across the eight ETFs is used to examine systematic exposures at the portfolio level.

The static factor model explains **89.82%** of portfolio return variation.

The portfolio exhibits:

- Positive market exposure.
- Negative sensitivity to changes in the VIX.
- Negative interest-rate exposure.
- Negative U.S. dollar exposure.
- Positive commodity exposure.

The rolling portfolio R-squared averages **88.88%**, ranging from **77.31% to 95.49%**.

## Systematic Risk Attribution

![Portfolio Factor Risk Attribution](figures/portfolio_factor_risk_attribution.png)

The static systematic variance decomposition shows:

| Factor | Share of Systematic Risk |
|---|---:|
| MKT | 67.96% |
| COM | 21.61% |
| VIX | 4.37% |
| USD | 3.27% |
| RATE | 2.80% |

Despite holding eight assets across several asset classes, approximately **89.6% of systematic portfolio risk is associated with the market and commodity factors combined**.

This illustrates an important portfolio-management principle:

> **Asset diversification does not necessarily imply factor diversification.**

## Dynamic Risk Attribution

![Rolling Portfolio Factor Risk](figures/rolling_portfolio_factor_risk.png)

The composition of systematic portfolio risk is not constant through time.

Across rolling windows, the market factor contributes an average of **65.43%** of systematic variance, while the commodity factor contributes **23.42%**.

Changes in both factor sensitivities and factor covariance structures cause the underlying sources of portfolio risk to evolve across market environments.

## Stress Regimes

![Stress Factor Risk Attribution](figures/stress_factor_risk_attribution.png)

The composition of systematic risk differs materially across the selected stress periods.

| Period | MKT | VIX | RATE | USD | COM |
|---|---:|---:|---:|---:|---:|
| COVID-19 Shock | 80.50% | 6.99% | -5.74% | 0.23% | 18.02% |
| 2022 Tightening Shock | 60.32% | 8.90% | 3.68% | 4.45% | 22.65% |
| 2025 Market Uncertainty | 61.41% | -0.08% | 4.52% | 3.30% | 30.86% |

Negative contributions may arise because factor covariances can partially offset systematic portfolio variance.

The results demonstrate that financial stress is not a single homogeneous regime. The relative importance of market, commodity, volatility, interest-rate, and currency risk changes depending on the financial environment.

## Key Findings

- Factor exposures differ substantially across asset classes.
- Static betas can conceal meaningful changes in exposure intensity through time.
- Several economically important exposures remain highly persistent in direction.
- Diversification across assets partially stabilizes portfolio-level factor exposures.
- The five-factor model explains almost 90% of the equal-weight portfolio's return variation.
- Market risk is the dominant systematic driver, followed by commodity risk.
- A diversified portfolio can remain highly concentrated in a small number of systematic risk factors.
- The composition of systematic risk changes materially across market regimes.

## Portfolio Management Implications

The analysis highlights why portfolio risk should not be evaluated exclusively through total volatility or static asset correlations.

Factor analysis provides an additional layer of information by identifying the economic sources underlying portfolio fluctuations.

For portfolio construction and risk management, this means that diversification should be evaluated not only across securities and asset classes, but also across the systematic factors that ultimately drive portfolio risk.

## Repository Structure

```text
factor-risk-analysis/
│
├── data/
│   ├── prices_clean.csv
│   └── factors_clean.csv
│
├── figures/
│
├── 03_factor_risk_analysis.ipynb
├── README.md
└── requirements.txt
```

## Technologies

- Python
- pandas
- NumPy
- SciPy
- statsmodels
- Matplotlib
- yfinance

## Disclaimer

This project is intended for educational and portfolio purposes. Results should not be interpreted as investment advice.