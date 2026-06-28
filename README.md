# NHANES Exploratory Data Analysis

An exploratory data analysis (EDA) project on the **National Health and Nutrition Examination Survey (NHANES)** dataset sourced from [Kaggle](https://www.kaggle.com/code/lalina/exploratory-data-analysis-project). The dataset contains health, lifestyle, and body measurement data collected from US adults by the CDC. This project explores distributions, outliers, correlations, and group differences across variables like BMI, smoking status, age, and gender — and tests three statistical hypotheses using proportion z-tests, chi-square, and independent t-tests.

---

## Dataset

The NHANES dataset is a programme of studies conducted by the US Centers for Disease Control and Prevention (CDC) designed to assess the health and nutritional status of adults and children in the United States.

| Property | Value |
|---|---|
| Source | CDC / NHANES |
| Raw rows | 5,735 |
| Raw columns | 28 |
| Rows after cleaning | 5,171 |
| Columns used | 8 |

### Columns selected

| Original column | Renamed to | Description |
|---|---|---|
| `SEQN` | `id` | Respondent ID (dropped before analysis) |
| `SMQ020` | `smoking` | Smoked at least 100 cigarettes (Yes / No) |
| `RIAGENDR` | `gender` | Gender (Male / Female) |
| `RIDAGEYR` | `age` | Age in years |
| `DMDEDUC2` | `education` | Highest education level |
| `BMXWT` | `weight` | Weight in kg |
| `BMXHT` | `height` | Height in cm |
| `BMXBMI` | `bmi` | Body Mass Index |

---

## Project structure

```
nhanes-eda/
│
├── NHANES.csv                  # Raw dataset
├── nhanes_eda_project.ipynb    # Main analysis notebook
└── README.md
```

---

## Analysis steps

### 1. Data overview
- Checked shape, column names, and data types
- Previewed raw data with `head()` and `info()`
- Checked for duplicate rows — none found

### 2. Data cleaning
- Dropped the `id` column (not needed for analysis)
- Checked missing values as a percentage per column
- Dropped rows with any null values (5,735 → 5,406 rows)
- Mapped numeric codes to readable labels for `smoking`, `gender`, and `education`

### 3. Outlier detection and removal
Used the **IQR method** (lower = Q1 − 1.5×IQR, upper = Q3 + 1.5×IQR) on three columns:

| Column | Outliers removed |
|---|---|
| `height` | 4 |
| `weight` | 151 |
| `bmi` | 80 |

Final clean dataset: **5,171 rows**

### 4. Distribution analysis
- Histograms with KDE curves for age, weight, height, and BMI — before and after outlier removal
- Boxplots to visualise spread and confirm outlier removal

### 5. Correlation analysis
- Correlation heatmap (`coolwarm`) across all numerical columns
- Pairplot split by gender
- Pairplot split by smoking status

### 6. Group comparisons
- Age binned into decade bands: (18–30], (30–40], (40–50], (50–60], (60–70], (70–80]
- Smoking proportion and group size by age band and gender
- Mean and standard deviation of weight, height, and BMI by age band and gender
- Cross-tabulation of gender vs age band

---

## Hypotheses and statistical tests

### H01 — Obesity in females aged 40–50
> **H₀:** Females aged 40–50 are not predominantly obese (BMI ≤ 30)
> **H₁:** Females aged 40–50 are predominantly obese (BMI > 30)

**Test:** One-sample proportion z-test (`proportions_ztest`)
**Result:** 224 out of 469 females aged 40–50 had BMI > 30 (47.8%)

---

### H02 — Smoking rates by gender
> **H₀:** The proportion of male smokers does not differ significantly from female smokers
> **H₁:** The proportion of male smokers differs significantly from female smokers

**Test:** Chi-square test of independence (`chi2_contingency`)
**Observed rates:** Male 53.3% | Female 31.2%

---

### H03 — BMI by gender
> **H₀:** The BMI of males and females is statistically similar
> **H₁:** The BMI of males and females is statistically different

**Test:** Independent samples t-test (`ttest_ind`)
**Observed means:** Male 28.21 | Female 29.09

---

## Libraries used

```python
pandas
numpy
matplotlib
seaborn
scipy
statsmodels
```

---

## How to run

1. Clone the repository
```bash
git clone https://github.com/EricMWaimiri/nhanes-eda.git
cd nhanes-eda
```

2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn statsmodels
```

3. Open the notebook
```bash
jupyter notebook nhanes_eda_project.ipynb
```

4. Update the file path in the second cell to point to your local copy of `NHANES.csv`
```python
path = r'your/local/path/to/NHANES.csv'
```

---

## Author

**Eric Waimiri**
[GitHub](https://github.com/EricMWaimiri)
