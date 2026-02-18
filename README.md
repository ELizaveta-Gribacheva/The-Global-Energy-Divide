# Data Cleaning & Preprocessing: Global Energy Indicators

This repository contains the data preparation and cleaning phase for a project analyzing sustainable development and global energy indicators (2000–2020). The primary goal was to transform raw, noisy datasets into a validated format optimized for advanced visualization in Tableau.

## Data Dictionary

| Column | Description |
| :--- | :--- |
| **Entity** | Country or region name. |
| **Year** | Observation year (2000–2020). |
| **Latitude / Longitude** | Geographic coordinates for mapping. |
| **Land Area (Km2)** | Total land area of the entity. |
| **Density (P/Km2)** | Population density (people per sq. km). |
| **Access to electricity (%)** | Percentage of the population with grid access. |
| **Access to clean fuels** | % of the population using clean cooking fuels. |
| **Renewable capacity** | Renewable energy capacity per capita. |
| **Renewable energy share** | Share of renewables in total final energy consumption. |
| **Electricity from...** | Generation from Fossil fuels, Nuclear, and Renewables. |
| **Low-carbon electricity** | Combined share of Nuclear and Renewables in total generation. |
| **Primary energy per capita** | Energy consumption per person (kWh/person). |
| **Energy intensity** | Energy used per unit of GDP. |
| **Value_co2_emissions** | CO2 emissions per capita (metric tons). |
| **GDP per capita** | Gross Domestic Product per person. |
| **GDP growth** | Annual GDP growth rate (%). |

## Data Cleaning Methodology

### 1. Advanced Imputation (IterativeImputer)
To handle missing values, I utilized the **IterativeImputer** from Scikit-learn, moving beyond simple mean/median filling.
* **Why this method:** It treats each feature with missing values as a function of others. This is crucial for energy data where metrics like GDP, energy consumption, and CO2 emissions are highly correlated.
* **The Process:** The imputer models each feature with missing values as a regression of other features in a round-robin fashion, preserving the statistical integrity of the multi-dimensional dataset.

### 2. Transformation & Validation
* **CO2 Per Capita Calculation:** Validated and processed the `Value_co2_emissions` metric to represent metric tons per person, enabling a fair comparison between countries of different population sizes.
* **Correlation Analysis (Linear & Logarithmic):** * Performed **Linear Correlation** (Pearson) to identify direct relationships between energy access and economic growth.
    * Applied **Logarithmic Transformation** to handle skewed data, particularly for GDP and CO2 emissions, allowing for a more accurate visualization of exponential trends and diminishing returns in human welfare metrics.
* **Duplicate Removal:** Identified and removed redundant records to ensure unique Entity-Year entries.
* **Type Casting:** Converted object types to numeric (float/int) for mathematical accuracy in correlation analysis.

## Tech Stack
* **Language:** Python
* **Libraries:** Pandas, NumPy, Scikit-learn (IterativeImputer)
* **Environment:** Cursor / VS Code
