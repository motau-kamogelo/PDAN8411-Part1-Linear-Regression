# Medical Insurance Cost Prediction Report
## Linear Regression Analysis

**Client:** South African Medical Aid Scheme  
**Student:** Kamogelo Motau (ST10500865)
**Date:** March 18, 2026

---
## This report covers the following:
1. Data cleaning steps

2. EDA with key visualizations described

3. Feature selection process

4. Model training approach

5. Evaluation metrics and interpretation

6. Business insights

7. Recommendations

---

## 1. Executive Summary

A linear regression model was developed to predict medical insurance charges. The model explains **78% of charge variance** with an average error of **$4,200**.

**Key Drivers:**
- **Smoking:** +$23,600
- **Age:** +$257/year
- **BMI:** +$329/unit

---

## 2. Data Cleaning

**Dataset:** 1,338 US insurance records, 7 features, no missing values

**Actions Taken:**
- Verified data types
- No missing values to impute
- No duplicates found
- Outliers retained (represent real cases)

**Result:** Clean dataset ready for analysis

---

## 3. Exploratory Data Analysis

### Key Visualizations & Findings

**1. Target Variable Distribution**
- Charges are right-skewed (mean $13,270, range $1,121-$63,770)
- High-cost outliers present (3.4%)

**2. Smoking Impact**
- Smokers pay ~4× more than non-smokers
- Strongest predictor (correlation 0.79)

**3. Age & BMI Effects**
- Age: $260 increase per year
- BMI: $330 increase per unit
- Smoking amplifies BMI impact (r=0.55 for smokers vs 0.08 for non-smokers)

**4. Regional Variation**
- Minimal impact (<$1,000 difference)
- Northeast lowest, Southwest highest

**5. Gender**
- Not statistically significant (p=0.094)

---

## 4. Feature Engineering & Selection

**Encoding:**
- Sex: male=1, female=0
- Smoker: yes=1, no=0
- Region: One-hot encoded (southwest reference)

**Feature Selection (p-value based):**

| Feature | P-Value | Selected |
|---------|---------|----------|
| smoker | <0.001 | ✓ |
| age | <0.001 | ✓ |
| bmi | <0.001 | ✓ |
| children | <0.001 | ✓ |
| region_northeast | 0.021 | ✓ |
| region_northwest | 0.045 | ✓ |
| region_southeast | 0.042 | ✓ |
| sex | 0.094 | ✗ |

**VIF Check:** All VIF < 10 (no multicollinearity)

**Final Features (7):** age, bmi, children, smoker, region_northeast, region_northwest, region_southeast

---

## 5. Model Training

**Data Split:** 80% train (1,070), 20% test (268)

**Models Tested:**
- Linear Regression (baseline)
- Ridge Regression (α=1.0)
- Lasso Regression (α=1.0)
- Polynomial Ridge (degree 2)

**Cross-Validation (5-fold):**

| Model | CV R² | Test R² |
|-------|-------|---------|
| Linear Regression | 0.77 ± 0.02 | 0.78 |
| Ridge | 0.77 ± 0.02 | 0.78 |
| Lasso | 0.76 ± 0.03 | 0.77 |
| Polynomial Ridge | 0.78 ± 0.02 | 0.79 |

**Selected:** Linear Regression (simplest, interpretable, competitive performance)

---

## 6. Model Evaluation

### Performance Metrics

| Metric | Value | Interpretation |
|--------|-------|----------------|
| R² | 0.78 | Explains 78% of charge variance |
| RMSE | $5,812 | Typical error magnitude |
| MAE | $4,215 | Average prediction error |

### Residual Analysis

- Mean residual: -$23 (unbiased)
- Residuals approximately normal
- Slight heteroscedasticity at high values

**Accuracy by Charge Level:**

| Charge Range | MAE |
|--------------|-----|
| $1K-$10K | $1,850 |
| $10K-$20K | $3,420 |
| $20K-$30K | $4,890 |
| $30K+ | $8,750 |

---

## 7. Model Interpretation

### Final Equation
Charges = -11,500 + 257×age + 329×bmi + 475×children + 23,600×smoker - 950×region_NE - 500×region_NW - 300×region_SE


### Business Insights

| Factor | Impact | Business Implication |
|--------|--------|---------------------|
| **Smoking** | +$23,600 | Primary pricing differentiator |
| **Age** | +$257/year | Age-based tiers justified |
| **BMI** | +$329/unit | Wellness programs valuable |
| **Children** | +$475/child | Moderate family impact |
| **Region** | -$300 to -$950 | Minor adjustments only |

---

## 8. Recommendations

### Immediate Actions

1. **Deploy model** as pricing guidance tool
2. **Implement smoking-based tiers** (smokers pay ~4× non-smokers)
3. **Create age brackets:**
   - 18-30: 0.8× baseline
   - 31-45: 1.0× baseline
   - 46-60: 1.3× baseline
   - 60+: 1.6× baseline
4. **Launch BMI wellness program** with premium incentives

### Future Improvements

1. **Collect South African data** for model retraining
2. **Add features:** pre-existing conditions, exercise habits
3. **Develop segmented models** (smokers vs non-smokers)
4. **Test non-linear models** (Random Forest, XGBoost)

---

## 9. Limitations

| Limitation | Impact |
|------------|--------|
| US-based data | May not reflect SA market |
| Linear assumption | Misses complex patterns |
| Limited features | No health history data |
| Cross-sectional | No trend analysis |
