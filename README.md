# Assessing the Economic Returns of Broadband: Cross-Country Evidence from the Broadband Boom Era (1995–2015)
Empirical analysis of broadband penetration and GDP per capita growth across countries (1995–2015), using World Bank data and regression-based model selection and validation techniques.

---

## Project Overview

This project empirically investigates the relationship between broadband penetration and cross-country GDP per capita growth during the global broadband expansion period from 1995 to 2015. Using a panel dataset of 217 countries drawn from the World Bank’s *World Development Indicators*, the analysis applies linear regression techniques combined with systematic data preprocessing, model selection, and validation procedures.

Motivated by development economics and ICT-growth literature, the study evaluates whether broadband diffusion meaningfully explains variation in economic growth across countries once standard macroeconomic, demographic, and institutional controls are accounted for. Particular emphasis is placed on identifying regional heterogeneity in broadband’s economic returns, recognizing that the growth effects of digital infrastructure may depend on underlying development conditions and complementary institutions.

---

## Research Question

**How well does broadband penetration explain cross-country variation in GDP per capita growth, controlling for key macroeconomic and demographic factors during the broadband boom era (1995–2015)?**

Based on prior literature, the analysis evaluates the following expectations:

* Broadband penetration contributes positively to GDP per capita growth, but not uniformly across regions
* Returns to broadband exhibit threshold effects, strengthening after widespread adoption
* Traditional growth determinants (capital formation, population growth, urbanization) remain key predictors of economic performance
* Regional context moderates the relationship between broadband diffusion and economic growth

---

## Data Sources

### World Development Indicators (WDI) – World Bank

* **Coverage:** 217 countries, 1995–2015
* **Observations:** 4,557 country-year observations
* **Source:** World Bank (2025), *World Development Indicators*

The dataset includes standardized country-level indicators compiled from national statistical offices, household and firm surveys, administrative records, and international organizations.

### Key Variables

* **Response Variable:**

  * GDP per capita growth (annual %)
* **Broadband and ICT Indicators:**

  * Fixed broadband subscriptions
  * Mobile cellular subscriptions
  * Internet usage rates
* **Control Variables:**

  * Gross capital formation
  * Inflation
  * Population growth
  * Urban population share
  * School enrollment
  * Institutional indicators (initially considered)

The panel structure enables estimation of broadband’s marginal contribution to economic growth over time.

---

## Data Preparation

The data preparation pipeline follows a structured and transparent workflow:

### 1. Data Cleaning

* Observations missing **all predictor values** were removed
* Remaining missing predictor values were imputed using **median substitution**
* Country-year observations were retained only when GDP growth data were available

### 2. Interpolation and Transformation

* Missing values in time-series predictors were interpolated where appropriate
* GDP per capita growth was transformed to address non-normality:

  * A constant was added to ensure positivity
  * A power transformation (exponent = 2/3) was applied, as suggested by the `powerTransform` function

### 3. Train–Test Split

* Data were split into:

  * **Training set:** 80% (n = 2,672)
  * **Testing set:** 20% (n = 669)
* A two-sample t-test confirmed that training and testing sets were drawn from the same distribution (p = 0.603)

---

## Modeling Framework

The core empirical strategy employs **multiple linear regression** to estimate the association between broadband diffusion and GDP per capita growth.

### Baseline Specification

$$GDPGrowth_{it} = \beta_0 + \beta_1 Broadband_{it} + \beta_2 ICT_{it} + \beta_3 X_{it} + \varepsilon_{it}$$

Where:

* $$Broadband_{it}$$ captures broadband penetration measures
* $$ICT_{it}$$ includes mobile and internet usage indicators
* $$X_{it}$$ represents macroeconomic and demographic controls

### Model Selection

* Backward elimination was used to refine the model
* Variables such as **FDI**, **Trade-to-GDP**, and **Rule of Law** were removed
* Removal was validated using a **partial F-test** (F = 1.49, df = 3, p = 0.216)

The final specification balances explanatory power with parsimony.

---

## Model Diagnostics and Validation

Model adequacy was evaluated using standard regression diagnostics:

* **Leverage:** Identification of high-leverage observations
* **Influence:** Cook’s distance, DFFITS, and standardized residuals
* **Assumption checks:** Linearity, homoscedasticity, and normality

While a large number of high-leverage points were observed (typical in cross-country macro data), relatively few observations were found to be influential.

### Out-of-Sample Performance

* Model fit on the testing set explains approximately **14%** of variation in the transformed GDP growth response (R^2 = 0.1414)
* Predictive performance is modest but consistent with expectations for macroeconomic cross-country regressions

---

## Results

### Key Findings

* **Broadband penetration is not a globally significant predictor** of GDP per capita growth once controls are included
* **Regional heterogeneity is substantial**:

  * **Positive broadband–growth relationships:**
    * Middle East & North Africa
    * Sub-Saharan Africa
    * East Asia & Pacific
      
  * **Weak or negative relationships:**
    * Europe & Central Asia
    * North America
    * Latin America & Caribbean
    * South Asia

### Other Important Predictors

* **Positive predictors:**
  * Gross capital formation
  * Urbanization
  * Population growth
    
* **Negative predictors:**
  * Inflation
  * Certain demographic pressures

These findings suggest that broadband’s economic returns depend critically on regional development conditions and complementary infrastructure.

---

## Limitations

Several limitations should be noted:

* Median imputation may understate uncertainty and attenuate variability
* Cross-country heterogeneity limits the interpretability of a single global model
* Temporal correlation within countries is assumed to be minimal
* The model relies on a single train–test split rather than full cross-validation

Future extensions could employ multiple imputation, region-specific models, and resampling-based validation.

---

## Repository Structure

```
Broadband_GDP_Growth_Analysis/
├── 302 R file.Rmd              # Main analysis code
├── 302 Poster.pdf              # Final research poster
├── Broadband.csv               # Raw broadband dataset
├── broadband_final.csv         # Cleaned and processed dataset
├── metadata.csv                # Variable definitions
└── README.md                   # Project documentation
```

---

## How to Reproduce

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/Assessing_Economic_Returns_of_Broadband.git
cd Assessing_Economic_Returns_of_Broadband
```

### 2. Install Required R Packages

```r
install.packages(c(
  "tidyverse",
  "car",
  "MASS",
  "caret",
  "ggplot2"
))
```

### 3. Run the Analysis

* Open `302 R file.Rmd` in RStudio
* Click **Render**

The script:

* Loads and cleans WDI data
* Performs imputation and transformation
* Fits and selects regression models
* Conducts diagnostic checks
* Produces tables and figures used in the final poster

---

## Citations

1. Czernich, N., Falck, O., Kretschmer, T., & Woessmann, L. (2011). Broadband infrastructure and economic growth. *The Economic Journal, 121*(552), 505–532. [https://www.jstor.org/stable/41236989](https://www.jstor.org/stable/41236989)

2. Holt, L., & Jamison, M. (2009). Broadband and contributions to economic growth: Lessons from the US experience. *Telecommunications Policy, 33*(10), 575–581. [https://doi.org/10.1016/j.telpol.2009.08.008](https://doi.org/10.1016/j.telpol.2009.08.008)

3. Koutroumpis, P. (2009). The economic impact of broadband on growth: A simultaneous approach. *Telecommunications Policy, 33*(9), 471–485. [https://doi.org/10.1016/j.telpol.2009.07.004](https://doi.org/10.1016/j.telpol.2009.07.004)

4. Minges, M. (2016). *Exploring the relationship between broadband and economic growth*. World Bank.
   [https://documents1.worldbank.org/curated/en/178701467988875888/pdf/102955-WP-Box394845B-PUBLIC-WDR16-BP-Exploring-the-Relationship-between-Broadband-and-Economic-Growth-Minges.pdf](https://documents1.worldbank.org/curated/en/178701467988875888/pdf/102955-WP-Box394845B-PUBLIC-WDR16-BP-Exploring-the-Relationship-between-Broadband-and-Economic-Growth-Minges.pdf)

5. Prieger, J. E. (2013). The broadband digital divide and the economic benefits of mobile broadband for rural areas. *Telecommunications Policy, 37*(6–7), 483–502. [https://doi.org/10.1016/j.telpol.2012.11.003](https://doi.org/10.1016/j.telpol.2012.11.003)

6. Qiang, C. Z., Rossotto, C. M., & Kimura, K. (2009). Economic impacts of broadband. In *Information and communications for development 2009: Extending reach and increasing impact* (pp. 35–50). World Bank / Oxford University Press.
   [https://thedocs.worldbank.org/en/doc/834151434649067733-0190022009/original/IC4DBroadband3550.pdf](https://thedocs.worldbank.org/en/doc/834151434649067733-0190022009/original/IC4DBroadband3550.pdf)

### Dataset

7. World Bank. (2025). *World Development Indicators*. The World Bank.
   [https://databank.worldbank.org/source/world-development-indicators](https://databank.worldbank.org/source/world-development-indicators)

---
