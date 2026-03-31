# Medical Insurance Cost Prediction Project
## Linear Regression Analysis Report

**Prepared For:** South African Medical Aid Scheme  
**Prepared By:** Kamogelo Motau 
**Date:** March 18, 2026  
**Project:** Insurance Charges Prediction Model

---

## 1. Executive Summary

This project developed a linear regression model to predict medical insurance charges for the South African medical aid scheme. Using a dataset of 1,338 US-based insurance customers, we built a model that explains **78% of the variance in insurance charges** with an average prediction error of **$4,200**.

### Key Business Insights:
- **Smoking status** is the strongest predictor, increasing charges by approximately **$23,600**
- **Age** increases charges by **$260 per year**
- **BMI** adds **$330 per unit** above normal range
- **Geographic region** has minimal impact (<5% variation)
- **Gender was not statistically significant** (p > 0.05)

### Model Performance:
| Metric | Value |
|--------|-------|
| R-squared (R²) | 0.78 |
| RMSE | $5,800 |
| MAE | $4,200 |
| Cross-validation R² | 0.77 ± 0.04 |

---

## 2. Introduction & Business Problem

### Business Context
The medical aid scheme requires a sliding scale of charges based on customer demographics, lifestyle factors, and geographic location. This model will help:
- Tailor insurance costs to individual risk profiles
- Develop fair pricing strategies
- Identify key cost drivers for better risk management
- Support data-driven decision making for premium calculations

### Project Objectives
1. Create a predictive model for insurance charges
2. Identify the most important factors affecting costs
3. Provide interpretable results for business stakeholders
4. Establish a foundation for South African market adaptation

---

## 3. Data Cleaning & Preparation

### 3.1 Initial Data Overview

**Dataset Information:**
- **Source:** US-based medical insurance dataset
- **Sample Size:** 1,338 records
- **Features:** 7 variables (age, sex, bmi, children, smoker, region, charges)
- **Target Variable:** Insurance charges (continuous)
