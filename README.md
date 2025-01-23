
# Testing for Demographic Stochasticity in Settlement Dynamics

This repository supports the analyses detailed in Wachtel et al. (2025): *Ancient Levantine Demography Follows Ecological Stochasticity*. It includes the required data and code to ensure full transparency and reproducibility of the work.

---

## **1. Introduction**
This repository contains one script file and a `data` folder with 9 supporting files. The analyses test hypotheses about settlement dynamics using environmental and demographic data. The code is compatible with Python 3.12.7 and relies on the following package versions:

- `numpy==1.26.4`
- `pandas==2.2.2`
- `scikit-learn==1.5.1`
- `statsmodels==0.14.2`
- `imbalanced-learn==0.12.3`
- `matplotlib==3.9.2`
- `scipy==1.13.1`
- `openpyxl==3.1.5`

### **Note**
- A detailed description of the dataset and methodologies is included in the supplementary file *Supporting Information Text and Tables*, available with the publication.
- Since the procedures for hypotheses 1 (Random Forest) and 3 (selection of random points) include random components, the results may be different in terms of absolute values than those presented in Wachtel et al. (2025). However, the results should agree with the significant findings discussed in the paper (e.g. population size being the most important feature).

---

## **2. Dataset**
The script requires the following files located in the `data` folder:

### **2.1. Settlement Data**
**`Settlement_Data.xlsx`** includes settlement data divided into the following sheets:

- **`Early Periods`**: Data from the 5th to 3rd millennia BCE, including:
  - `Heb_Name`: Site name in Hebrew.
  - `POINT_X`, `POINT_Y`: Coordinates (New Israeli Grid).
  - `size(ha)`: Site area in hectares.
  - Period indicators (e.g., `Late_Chal`, `EBI`): 1 = inhabited, 0 = uninhabited.
  - Environmental attributes such as:
    - `NEAR_Spring`: Distance to the nearest spring.
    - `Height`: Elevation above sea level.
    - `Slope_100`: Slope at the settlement location.
    - `Percip_*`: Rainfall levels across different periods of the year.
    - `NEAR_Sea` and `NEAR_Chlak`: Distances to the sea and soft rock formations.

- **`1596`, `1881`, `1931`**: Historical village data from the Ottoman, PEF, and Mandate periods, respectively, with fields for village name ('Village'), location ('POINT_X', 'POINT_Y'), population size ('Population'), persistence status ('Continued'), and environmental attributes (as detailed above).

### **2.2. Niche Maps**
Files such as `1596_map.csv` and `1881_map.csv` provide simulated ecological niche maps for each period, with fields for:
- `POINT_X`, `POINT_Y`: Coordinates (New Israeli Grid).
- `Niche`: 1 = part of a niche, 0 = not part of a niche.

---

## **3. Analysis and Hypotheses**

### **3.1. Hypothesis 1: Small Population and Extinction**
**Goal**: Assess the relationship between population size and settlement abandonment.

**Steps**:
1. Identify abandoned settlements for each period.
2. Perform a two-way ANOVA on settlement size (early periods) or population size (later periods) and abandonment status.
3. For later periods:
   - Balance the data using Random Oversampling.
   - Compare Dummy Classifier and Random Forest models.
   - Evaluate feature importance.

**Output**: ANOVA results and feature importance chart.

---

### **3.2. Hypothesis 2: Niche Distribution Stability**
**Goal**: Test the stability of ecological niches across periods.

**Steps**:
1. Use MaxEnt to generate ecological niche maps (external process).
2. Compute Kappa statistics for niche similarity.
3. Compute Kappa statistics for settlement similarity.

**Output**: Kappa scores for niche and settlement stability.

---

### **3.3. Hypothesis 3: Proximity and Colonization**
**Goal**: Analyze the relationship between proximity to existing settlements and colonization probability.

**Steps**:
1. Simulate settlement data for each period:
   - Randomly sample new settlements and random points and compare average distances to the five nearest settlements.
2. Perform a two-way ANOVA to analyze settlement patterns.

**Output**: ANOVA results.

---

## **4. Setup and Usage**
1. Create a Python 3.12.7 environment.
2. Ensure the `data` folder is in the same directory as the script (or update the script to match your directory structure).
3. Load the script in Jupyter Notebook or a similar environment.
4. Install the required packages, if needed (first command in the script)
5. Execute the code step-by-step to reproduce the analyses.

---
