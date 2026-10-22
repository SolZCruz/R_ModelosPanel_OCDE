[Español](resultados.md) | **English**

# Panel Data Workshop: Fixed Effects vs. Random Effects

## Technology and Labor Productivity in OECD Countries

---

## 1. Research question

Do internet penetration and access to technology explain labor productivity better than traditional physical and institutional investment, in a panel of OECD countries?

Specific formulation: to what extent are internet access, electrification, investment in human capital (tertiary education) and R&D spending associated with labor productivity (GDP per person employed), and how do these estimates change when controlling for unobserved heterogeneity across countries (fixed effects) versus assuming that this heterogeneity is random (random effects)?

---

## 2. Data

**Source:** World Development Indicators (WDI), World Bank Data Bank

**Panel structure:** balanced, 26 OECD countries × 13 years (2007-2019) = 338 observations

| Role | Variable | WDI code |
|---|---|---|
| Dependent | GDP per person employed (constant, PPP) | `SL.GDP.PCAP.EM.KD` |
| Regressor | Individuals using the Internet (% of population) | `IT.NET.USER.ZS` |
| Regressor | Access to electricity (% of population) | `EG.ELC.ACCS.ZS` |
| Regressor | Tertiary school enrollment (% gross) | `SE.TER.ENRR` |
| Regressor | R&D expenditure (% of GDP) | `GB.XPD.RSDV.GD.ZS` |

**Methodological note:** 12 OECD countries\* were excluded because of missing data on tertiary enrollment and/or R&D expenditure, prioritizing keeping the panel balanced.

\*Australia, Costa Rica, Luxembourg, Japan, Iceland, Greece, Germany, United States, Switzerland, Portugal, New Zealand, Netherlands.

---

## 3. Descriptive statistics

### Variation between countries vs. within each country (GDP per worker)

| Source of variation | Standard deviation |
|---|---|
| Between countries | 33,377 |
| Within each country (over time) | 6,670 |

The variation between countries is ~5 times larger than the variation within each country. Most of the differences in productivity are explained by structural differences between countries (rather than by year-to-year changes within the same country), which anticipates that the fixed effects estimator —which uses only the "within" variation— will work with relatively less information than the random effects estimator.

![See faceted chart: GDP per worker by country](output/figures/facetas_pib_trabajador.png)

![See scatter plot: internet vs. GDP per worker](output/figures/scatter_internet_pib.png)

---

## 4. Model results

### 4.1 Model comparison

| Model | Description |
|---|---|
| Pooled OLS | Ignores the panel structure; treats each country-year observation as independent |
| Fixed Effects (FE) | Controls for time-invariant heterogeneity within each country |
| Random Effects (RE) | Assumes the country effect is not correlated with the regressors |


### Model comparison: GDP per worker

| Variable | Pooled OLS (1) | Fixed Effects (2) | Random Effects (3) |
|---|---:|---:|---:|
| Internet | 806.79*** (125.61) | 435.61*** (51.69) | 427.96*** (52.06) |
| Electricity | 11,023.92*** (3,140.52) | -5,911.07*** (1,446.69) | -5,394.33*** (1,456.37) |
| Tertiary enrollment | -118.16 (107.90) | 102.14** (49.87) | 102.53** (50.28) |
| R&D expenditure | 6,238.88*** (1,591.68) | -2,066.07 (1,433.14) | -1,057.16 (1,403.00) |
| Constant | -1,066,337.00*** (308,445.60) | — | 598,224.00*** (144,024.00) |
| **Observations** | 338 | 338 | 338 |
| **R²** | 0.395 | 0.300 | 0.284 |
| **Adjusted R²** | 0.388 | 0.235 | 0.275 |

*Standard errors in parentheses. Significance: \*p<0.1; \*\*p<0.05; \*\*\*p<0.01*

### 4.2 Hausman test: FE vs. RE

- **H0:** the individual (country) effects are not correlated with the regressors → RE is valid and more efficient
- **Result:** p = 0.0312

Since p < 0.05, **H0 is rejected**. The assumption required for RE to be valid does not hold with these data: the country-specific effects are in fact correlated with the explanatory variables. **The Fixed Effects (FE) model is selected** as the correct specification.

---

## 5. Diagnostics and robustness

| Test | What it evaluates | p-value | Conclusion |
|---|---|---|---|
| Breusch-Pagan | Heteroskedasticity | 0.0025 | Homoskedasticity is rejected → use robust standard errors |
| Wooldridge (panel) | Serial autocorrelation | ≈ 0 | No autocorrelation is rejected → use robust standard errors |

Both diagnostics confirm the need to report robust standard errors, clustered by country (Arellano method). **Important:** these corrections do not change the magnitude of the estimated coefficients; they only correct the precision with which their standard errors are calculated.

---

## 6. Final results: Fixed Effects model with robust standard errors

| Variable | Coefficient | Standard error (robust) | t | p-value | Significance |
|---|---:|---:|---:|---:|:---:|
| Internet (% of population) | 435.61 | 166.21 | 2.62 | 0.0092 | ** |
| Electricity (% of population) | -5911.07 | 3111.83 | -1.90 | 0.0584 | . |
| Tertiary enrollment (% gross) | 102.14 | 94.42 | 1.08 | 0.2802 | — |
| R&D expenditure (% of GDP) | -2066.07 | 4795.03 | -0.43 | 0.6669 | — |

*Significance codes: \*\*\* p<0.001, \*\* p<0.01, \* p<0.05, . p<0.10*

### Interpretation by variable

**Internet — significant at 1%.** For each additional percentage point of the population with internet access, GDP per worker increases by 435.6 units on average (constant PPP), controlling for unobserved heterogeneity across countries. It is the only variable with robust evidence consistent with the workshop's hypothesis.

**Electricity — significant only at 10%, negative sign.** This result should be interpreted with caution: in OECD countries, access to electricity is close to 100% from the start of the panel, so there is very little variation *within* each country over time — precisely the only source of variation that the FE estimator uses. With so little movement in the variable, the coefficient is unstable and should not be interpreted as a credible causal effect.

**Tertiary enrollment — not significant.** There is no evidence, within this panel, that changes in tertiary enrollment within a country are associated with changes in its labor productivity.

**R&D expenditure — not significant.** Possible explanations: a lagged effect not captured by the model (R&D investment can take several years to show up in productivity), and/or low temporal variation within each country during the period.

---

## 7. Conclusion

The evidence from the panel of 26 OECD countries (2007-2019) partially supports the hypothesis that access to technology explains labor productivity: **internet is the only regressor with a positive, robust and statistically significant effect**, even after controlling for unobserved heterogeneity across countries and correcting for heteroskedasticity and serial autocorrelation. The traditional infrastructure and human capital/R&D variables considered in this model do not show a robust association with productivity in this specific panel — a valid result in itself, which distinguishes the role of each type of input rather than confirming a uniform hypothesis about "technology in general."

### Limitations to discuss

- Little temporal variation in electricity within OECD countries limits the interpretation of that coefficient
- The effect of R&D expenditure on productivity probably operates with a lag, which is not captured in this static specification
- The panel excludes 12 OECD countries because of missing data, which could introduce some selection bias toward countries with better statistical infrastructure

---

## 8. Full methodology (technical summary)

1. **Cleaning and reshaping** of World Bank Data Bank data (wide → long), removing metadata rows
2. **Panel declaration** (`pdata.frame`, country-year index)
3. **Descriptive statistics** and analysis of between/within-country variation
4. **Estimation** of Pooled OLS, Fixed Effects and Random Effects (`plm` package in R)
5. **Hausman test** to select the correct specification
6. **Diagnostics** for heteroskedasticity (Breusch-Pagan) and autocorrelation (Wooldridge)
7. **Final report** with robust standard errors clustered by country (Arellano method)
