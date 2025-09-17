# TFM \- Estimación y Modelado del Valor Empresarial/de Mercado de Jugadores NBA a partir de Datos Públicos: Un Enfoque Analítico y Predictivo Multidimensional

**Modelización, validación multi-horizonte y mini–app Shiny**

App online: [**https://pjlormol.shinyapps.io/App\_TFM/**](https://pjlormol.shinyapps.io/App_TFM/)  
Cuaderno Colab: [**https://colab.research.google.com/drive/1tfqGRBiGrSxnIOgKaMCzDy8JVy\_1obBU\#scrollTo=af0abebc**](https://colab.research.google.com/drive/1tfqGRBiGrSxnIOgKaMCzDy8JVy_1obBU#scrollTo=af0abebc)  
Carpeta del proyecto (Drive): [**https://drive.google.com/drive/u/0/folders/1\_uk3QcRl7Q3i1sxLi4cc8umIX3QYHasb**](https://drive.google.com/drive/u/0/folders/1_uk3QcRl7Q3i1sxLi4cc8umIX3QYHasb)

---

## 🌟 Resumen

Este trabajo construye una **medición operativa del valor empresarial del jugador** (USD) combinando rendimiento deportivo, señales de popularidad (Wikipedia/Google Trends) y contexto (tamaño de mercado). Incluye:

- **Cuaderno (Colab)** para ingesta, normalización, *scoring* (t→t+1), proyección multi-horizonte, backtesting y generación de artefactos.  
- **Mini–app R Shiny** para lectura ejecutiva (KPIs, rankings, riesgo–retorno, fichas por jugador).  
- **Informe LaTeX** con resultados y discusión.

---

## 📁 Estructura del repositorio

project-root/

├─ data/

│  ├─ raw/csv/                      \# Datos brutos (Kaggle / señales)

│  └─ processed/                    \# Datasets procesados (salidas)

├─ reports/                         \# Resultados (scoring, métricas, etc.)

├─ models/                          \# Modelos y pipelines (.joblib)

├─ scripts/

│  ├─ popularity\_metrics/           \# Notebooks para Wikipedia/Trends

│  └─ R\_Shiny\_app/                  \# App Shiny (app.R \+ 4 entradas)

└─ notebooks/

   └─ TFM\_Cuaderno\_Código\_Lorente\_Molina\_Pedro\_Jesús

### Entradas de la **app Shiny** (en la misma carpeta que `app.R`)

- `scoring_results_full_*.csv` — scoring (t→t+1) con `pred_usd`, `p10_usd`, `p90_usd`, `salary_usd_prev`  
- `scoring_multi_forecast_*.csv` — proyecciones multi–horizonte (media, P10, P90)  
- `mh_metrics.csv` — MAE, MAPE, cobertura, estabilidad (Jaccard) por h  
- `common_player_info.csv` — mapping jugador→equipo/posición

---

## 🔁 Reproducibilidad (3 pasos)

### 1\) Descargar el proyecto

- Descarga y descomprime desde **\[PON AQUÍ TU ENLACE A DRIVE\]** manteniendo la estructura (`data/`, `reports/`, `models/`, `scripts/`, …).  
- Los **datos brutos** no se redistribuyen por licencia. Si deseas ejecutarlo completamente en local, descarga los CSV de Kaggle (ver sección “Datos”).

### 2\) Ejecutar el **cuaderno** (Colab recomendado)

- Abre: [**https://colab.research.google.com/drive/1tfqGRBiGrSxnIOgKaMCzDy8JVy\_1obBU\#scrollTo=af0abebc**](https://colab.research.google.com/drive/1tfqGRBiGrSxnIOgKaMCzDy8JVy_1obBU#scrollTo=af0abebc)  
- Crea una **copia** en tu Drive y ejecútalo de arriba a abajo.  
- El cuaderno:  
  - instala dependencias,  
  - integra y normaliza datos para construir el *dataset maestro* (jugador–año),  
  - genera *scoring* (t→t+1) y predicciones multi–horizonte,  
  - calcula métricas (MAE, MAPE, Cobertura, Jaccard),  
  - crea salidas en `data/processed/` y `reports/`,

Con las **mismas entradas y parámetros**, las salidas son **reproducibles**.

### 3\) Usar la **mini–app Shiny**

- **Opción A (online):** abre [**https://pjlormol.shinyapps.io/App\_TFM/**](https://pjlormol.shinyapps.io/App_TFM/)  
- **Opción B (local):**  
  1. Sitúate en `scripts/R_Shiny_app/` con los **4 archivos de entrada** indicados arriba.  
  2. Ejecuta en R/RStudio:  
       
     \# En RStudio: abre app.R y pulsa "Run App"  
       
     \# o por terminal:  
       
     R \-e "shiny::runApp('scripts/R\_Shiny\_app', launch.browser=TRUE)"  
       
  3. Navega por las pestañas: KPIs, distribución, Top-N, ΔUSD, Pareto/treemap, posiciones, perfil de jugador (fan chart \+ ficha).

---

## 🧪 Versiones recomendadas

- **R** ≥ 4.2, paquetes: `shiny`, `bslib`, `tidyverse`, `lubridate`, `scales`, `plotly`, `gt`, `readxl`, `stringr`.  
- **Python** (si ejecutas local en vez de Colab): 3.10–3.11 con `pandas`, `numpy`, `scikit-learn`, `joblib`, etc. (el cuaderno instala lo necesario).

---

## 🗃️ Datos (origen y licencia)

Los datasets se emplean según los **Data Terms de Kaggle** y sus licencias particulares. Enlaces principales:

- General NBA: [https://www.kaggle.com/datasets/wyattowalsh/basketball/data](https://www.kaggle.com/datasets/wyattowalsh/basketball/data)  
- Salarios (2000–2025): [https://www.kaggle.com/datasets/ratin21/nba-player-salaries-2000-2025](https://www.kaggle.com/datasets/ratin21/nba-player-salaries-2000-2025)  
- Market Size (2022): [https://www.kaggle.com/datasets/ratin21/2022-nba-team-market-size](https://www.kaggle.com/datasets/ratin21/2022-nba-team-market-size)

Señales de popularidad obtenidas a través de interfaces públicas de **Wikimedia Pageviews** y **Google Trends** (uso conforme a sus términos).  
El proyecto **no** procesa PII sensible.

---

## 📦 “Paquete de artefactos” (para auditoría)

Guarda junto al PDF un `.zip` tipo `artifacts_TFM_YYYYMMDD.zip` con:

- `reports/`: *scoring*, multi–horizonte, métricas (`mh_metrics.csv`, `metrics_backtest_multihorizon.csv`), `scoring_inputs.csv` (si existe) y `run_manifest.json`.  
- `data/processed/`: `player_master_year.csv`, `team_mapping.csv` (y `player_team_year.csv`, si aplica).  
- `models/`: `model_*.joblib` y `pipeline_*.joblib`.  
- `scripts/R_Shiny_app/`: `app.R` \+ **las 4 entradas exactas** usadas.

Por licencia, **no** redistribuyas `data/raw/csv/`; remite a Kaggle.

---

## 🧭 Qué encontrarás en la app (guía rápida)

- **KPIs**: tamaño de muestra, mediana/IQR de valor, correlación con salario previo, valor/coste agregados, ΔUSD total, % infravalorados, Gini y Top-20%.  
- **Distribuciones**: histograma con opción de escala log para colas pesadas.  
- **Top-N** y **ΔUSD divergente**: priorización de inversión/renegociación.  
- **Bubble riesgo–retorno**: ΔUSD vs incertidumbre (tamaño=valor).  
- **Pareto y treemap**: concentración del valor y eficiencia por equipo.  
- **Posiciones y segmentos**: comparativas por rol.  
- **Perfil de jugador**: *fan chart* por horizonte \+ ficha de año actual.

---

## 📝 Créditos y uso

Trabajo de TFM — “Estimación y Modelado del Valor Empresarial/de Mercado de Jugadores NBA a partir de Datos Públicos: Un Enfoque Analítico y Predictivo Multidimensional”.  
Se respetan las licencias de Kaggle y términos de Wikimedia/Google Trends. Repositorio para **fines académicos/profesionales internos**.

---

## 📬 Contacto

- Autor: **Pedro Jesús Lorente Molina**  
- App online: [https://pjlormol.shinyapps.io/App\_TFM/](https://pjlormol.shinyapps.io/App_TFM/)  
- Colab: [https://colab.research.google.com/drive/1tfqGRBiGrSxnIOgKaMCzDy8JVy\_1obBU\#scrollTo=af0abebc](https://colab.research.google.com/drive/1tfqGRBiGrSxnIOgKaMCzDy8JVy_1obBU#scrollTo=af0abebc)  
- Carpeta del proyecto (Drive): [https://drive.google.com/drive/u/0/folders/1\_uk3QcRl7Q3i1sxLi4cc8umIX3QYHasb](https://drive.google.com/drive/u/0/folders/1_uk3QcRl7Q3i1sxLi4cc8umIX3QYHasb)

