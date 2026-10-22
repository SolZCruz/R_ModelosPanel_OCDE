[Español](README.md) | **English**

# Panel Data Workshop: Fixed Effects vs. Random Effects

Applied workshop on technology and labor productivity in OECD countries, using World Bank panel data (World Development Indicators).

## Research question

Do internet penetration and access to technology explain labor productivity better than traditional physical and institutional investment, in a panel of OECD countries?

## Data

- **Source:** World Development Indicators (WDI), World Bank Data Bank
- **Panel:** 26 OECD countries × 13 years (2007-2019), balanced, 338 observations
- **Dependent variable:** GDP per person employed (`GDP per person employed (constant 2021 PPP $)`)
- **Regressors:** internet (`Individuals using the Internet (% of population)`), electricity (`Access to electricity (% of population)`), tertiary enrollment (`School enrollment, tertiary (% gross)`), R&D expenditure (`Research and development expenditure (% of GDP)`)

## Project structure

```
├── data/
│   ├── processed/              # Clean, balanced panel, long format
│   └── raw/                    # Original CSVs downloaded from the World Bank (untouched)
├── output/
│   ├── figures/                # Exported charts (.png)
│   └── tables/                 # Results tables (.csv, .html) and saved models (.rds)
├── scripts/
│   ├── 01_limpieza.R           # Wide -> long, removes metadata rows
│   ├── 02_descriptivos.R       # Descriptive statistics and exploratory charts
│   ├── 03_modelos.R            # Pooled OLS, Fixed Effects, Random Effects, Hausman
│   └── 04_diagnosticos.R       # Heteroskedasticity, autocorrelation, robust standard errors
├── README.md                   # Spanish version
├── README.en.md                # English version
├── resultados.md               # Final document with the full results narrative (Spanish)
└── resultados.en.md            # Final document with the full results narrative (English)
```

## How to run the project

Requires R with the packages: `tidyverse`, `janitor`, `skimr`, `plm`, `collapse`, `stargazer`, `lmtest`.

```r
install.packages(c("tidyverse", "janitor", "skimr", "plm", "collapse", "stargazer", "lmtest"))
```

Run the scripts in order from the project's root folder (open the whole folder in VS Code so that relative paths work):

1. `scripts/01_limpieza.R`
2. `scripts/02_descriptivos.R`
3. `scripts/03_modelos.R`
4. `scripts/04_diagnosticos.R`

## Main result

Fixed Effects model (selected via the Hausman test, p = 0.0312), with standard errors that are robust and clustered by country. Internet was the only regressor with a positive and statistically significant effect on labor productivity (p = 0.0092). Full results and interpretation are in [`resultados.en.md`](resultados.en.md).
