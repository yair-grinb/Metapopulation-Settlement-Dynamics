# Integrated Explanations and Usage for Wachtel et al 2024 "Ancient Levantine demography follows ecological stochasticity" Script

This document combines detailed explanations of the analysis and a user guide for running the script. The aim is to ensure full transparency and reproducibility of the work.

---

## **1. Introduction**
This Python script supports the analysis for Wachtel et al 2024. It tests hypotheses about settlement dynamics using environmental and demographic data. The script includes data preprocessing, machine learning modeling, and visualization of results.

### Note:
Detailed explanations about the datasets and work processes are included with the article as a supplementary file titled 'Supporting Information text and tables.'

---

## **2. Datasets**
The script relies on three Excel files:
- **`Data S1.xlsx`**:
  - Settlement data from earlier periods (e.g., 5th to 3rd millennia BCE).
  - Fields include:
    - `Heb_Name`: Site name in Hebrew.
    - `POINT_X`, `POINT_Y`: Coordinates in the New Israeli Grid (Longitude and Latitude).
    - `size(ha)`: Site area in hectares.
    - Period indicators (`Late_Chal`, `EBI`, etc.): 1 = inhabited, 0 = uninhabited.

- **`Data S2.xlsx`**:
  - Historical village data from the Ottoman, PEF, and Mandate periods (split into three sheets).
  - Fields include:
    - `Name`/`Village`: Village name.
    - `POINT_X`, `POINT_Y`: Coordinates in the New Israeli Grid.
    - `Population_XXXX`: Population size in different years (e.g., 1596, 1881, 1931).

- **`Data S3.xlsx`**:
  - Environmental data for modeling (used in MaxEnt and Random Forest).
  - Fields include:
    - `POINT_X`, `POINT_Y`: Coordinates in the New Israeli Grid.
    - Environmental variables: Slope, elevation, distance to water, soil depth, rock type, etc.

---

## **3. Analysis and Hypotheses**

### **Hypothesis 1: Small Population and Extinction**
- **Goal**: Analyze the relationship between population size and settlement abandonment.
- **Steps**:
  1. Merge population data (`Data S1`) with environmental variables (`Data S3`).
  2. Balance the data using Random Oversampling.
  3. Train a Random Forest model and evaluate feature importance.
- **Output**:
  - Insights into significant variables (e.g., slope, precipitation) affecting settlement dynamics.

### **Hypothesis 2: Niche Distribution Stability**
- **Goal**: Assess the stability of ecological niches over time using MaxEnt and Kappa statistics.
- **Steps**:
  1. Generate simulated ecological niche maps for different periods.
  2. Compute Kappa statistics to evaluate niche similarity across periods.
  3. Validate niche stability by calculating overlap with new settlements.
- **Output**:
  - Kappa scores and niche overlap values.

### **Hypothesis 3: Proximity and Colonization**
- **Goal**: Investigate the relationship between proximity to existing settlements and colonization probability.
- **Steps**:
  1. Calculate distances between new settlements and the nearest existing settlements.
  2. Compare these distances with random points.
  3. Perform a Two-way ANOVA to test significance.
- **Output**:
  - Distance comparisons and ANOVA results.

---

## **4. How to Use This Script**

### **Required Files**
- Ensure the following files are available:
  - `Data S1.xlsx`
  - `Data S2.xlsx`
  - `Data S3.xlsx`

### **Setup**
1. Update the file paths in the script to match your local directory.
2. Install necessary Python libraries:
   ```bash
   pip install pandas numpy scikit-learn imbalanced-learn matplotlib
