# Taller de Modelos de Panel: Efectos Fijos vs. Efectos Aleatorios

Taller aplicado sobre tecnología y productividad laboral en países de la OCDE, usando datos de panel del Banco Mundial (World Development Indicators).

## Pregunta de investigación

¿La penetración de internet y el acceso a tecnología explican mejor la productividad laboral que la inversión física e institucional tradicional, en un panel de países de la OCDE?

## Datos

- **Fuente:** World Development Indicators (WDI), World Bank Data Bank
- **Panel:** 26 países de la OCDE × 13 años (2007-2019), balanceado, 338 observaciones
- **Variable dependiente:** PIB por persona empleada (`GDP per person employed (constant 2021 PPP $)`)
- **Regresores:** internet (`Individuals using the Internet (% of population)`), electricidad (`Access to electricity (% of population)`), matrícula terciaria (`School enrollment, tertiary (% gross)`), gasto en I+D (`Research and development expenditure (% of GDP)`)

## Estructura del proyecto

```
├── data/
│   ├── processed/              # Panel limpio, balanceado, formato largo
│   └── raw/                    # CSV originales descargados del Banco Mundial (sin tocar)
├── output/
│   ├── figures/                # Gráficos exportados (.png)
│   └── tables/                 # Tablas de resultados (.csv, .html) y modelos guardados (.rds)
├── scripts/
│   ├── 01_limpieza.R           # Ancho -> largo, elimina filas de metadatos
│   ├── 02_descriptivos.R       # Estadística descriptiva y gráficos exploratorios
│   ├── 03_modelos.R            # Pooled OLS, Efectos Fijos, Efectos Aleatorios, Hausman
│   └── 04_diagnosticos.R       # Heterocedasticidad, autocorrelación, errores robustos
├── README.md
└── resultados.md               # Documento final con narrativa completa de resultados
```

## Cómo correr el proyecto

Requiere R con los paquetes: `tidyverse`, `janitor`, `skimr`, `plm`, `collapse`, `stargazer`, `lmtest`.

```r
install.packages(c("tidyverse", "janitor", "skimr", "plm", "collapse", "stargazer", "lmtest"))
```

Correr los scripts en orden desde la carpeta raíz del proyecto (abrir la carpeta completa en VS Code para que los paths relativos funcionen):

1. `scripts/01_limpieza.R`
2. `scripts/02_descriptivos.R`
3. `scripts/03_modelos.R`
4. `scripts/04_diagnosticos.R`

## Resultado principal

Modelo de Efectos Fijos (seleccionado vía test de Hausman, p = 0.0312), con errores estándar robustos agrupados por país. El internet resultó ser el único regresor con efecto positivo y estadísticamente significativo sobre la productividad laboral (p = 0.0092). Detalle completo de resultados e interpretación en `resultados.md`.