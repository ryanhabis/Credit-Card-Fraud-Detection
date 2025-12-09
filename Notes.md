# Credit Card Fraud Detection - Analysis Report

## 📊 Project Overview
- **Objective:** Detect fraudulent credit card transactions using data analytics
- **Dataset:** 284,807 transactions from European cardholders (48-hour period)
- **Fraud Prevalence:** 0.17% (highly imbalanced dataset)
- **Framework:** CRISP-DM methodology
- **Author:** Ryan Habits

---

## 📈 Key Hypotheses & Results

| Hypothesis | Statistical Test | Result | P-Value | Conclusion |
|------------|------------------|--------|---------|------------|
| **H1:** Fraud amounts differ from legitimate transactions | Two-Sample T-Test (Welch's) | Fraud mean: €123.87 vs Normal: €88.41 | **0.0032** | ✅ **Supported** |
| **H2:** Fraud occurs more frequently at specific times | Time-series analysis | Peak at **11 AM** | - | ✅ **Supported** |
| **H3:** Undersampling reveals hidden fraud patterns | Model evaluation | Needs further validation | - | ⚠️ **Inconclusive** |

---

## 🔍 Top Fraud Predictors (Logistic Regression)

### Table A.2: Logistic Regression Coefficients

| Component | Coefficient | Interpretation |
|-----------|-------------|----------------|
| **V14** | **-0.8647** | **Strongest fraud predictor** |
| **V12** | **-0.7565** | Second strongest predictor |
| V16 | -0.2465 | Moderate predictor |
| V10 | -0.1775 | Weak predictor |
| V17 | +0.2167 | Positive relationship (unusual) |
| **Intercept** | **-2.3721** | Baseline fraud probability |

**Key Insight:** Negative coefficients indicate stronger relationship with fraud detection.

---

## 🎯 Model Performance Evaluation

### Table A.3: Logistic Regression Metrics

| Metric | Value | Interpretation |
|--------|-------|----------------|
| **Overall Accuracy** | 98.0% | Misleading due to class imbalance |
| **Recall (Detection Rate)** | **84.3%** | Captures majority of fraud cases |
| **Precision** | **9.2%** | High false positive rate |
| **F1-Score** | 0.166 | Poor precision-recall balance |

**Conclusion:** Model is **sensitive but not precise** - good recall but poor precision.

---

## 📊 Statistical Analysis Details

### Table A.4: T-Test Results (H1)
| Statistic | Value |
|-----------|-------|
| Normal Mean | €88.41 |
| Fraud Mean | €123.87 |
| Mean Difference | €35.46 (Fraud higher) |
| T-statistic | -2.961 |
| P-value | **0.0032** |
| Significance | p < 0.01 |

### Table A.5: ANOVA Results (V1 vs Amount Categories)
| Source | Sum of Squares | df | F-statistic | P-value |
|--------|----------------|----|-------------|---------|
| Between Groups | 39,721.22 | 3 | **3630.85** | **< 0.0001** |
| Within Groups | 1,028,040.00 | 281,914 | - | - |

### Table A.6: Transaction Amount Categories
| Category | Range (€) | Sample Size | Description |
|----------|-----------|-------------|-------------|
| Small | < 50 | 192,415 | Low-value transactions |
| Medium | 50-200 | 69,238 | Everyday purchases |
| Large | 200-1000 | 19,574 | High-value purchases |
| Very Large | > 1000 | 2,499 | Luxury transactions |

**ANOVA Insight:** V1 values differ significantly across transaction amounts (p < 0.0001).

---

## 🕒 Temporal Analysis
- **Fraud Start Time:** 1 AM - 2 AM
- **Peak Fraud Time:** **11 AM**
- **Pattern:** Clear temporal clustering of fraudulent transactions

---

## 🔗 Correlation Insights (Heatmap)
| Feature | Correlation with Fraud (Class) |
|---------|-------------------------------|
| V17 | **0.31** (Highest positive) |
| V14 | **0.29** |
| V12 | **0.25** |
| Amount | **0.01** (Very weak) |

**Key Finding:** Transaction amount alone is poorly correlated with fraud.

---

## 📝 Key Insights Summary

### ✅ What Works Well:
1. **V14 and V12 are excellent predictors** of fraud (strong negative coefficients)
2. **Model captures 84.3% of fraud cases** (good recall)
3. **Clear temporal patterns** - fraud peaks at 11 AM
4. **Statistical significance** confirmed for all major hypotheses

### ⚠️ Limitations:
1. **High false positive rate** (9% precision = 91% false alarms)
2. **Severe class imbalance** (0.17% fraud rate)
3. **Amount alone is insufficient** for fraud detection

### 🔄 Feature Importance Ranking:
1. **V14** (Most important)
2. **V12** (Second most important)
3. **V16, V10** (Moderate importance)
4. **Transaction Amount** (Low importance)
5. **Time** (Contextual importance)

---

## 💡 Recommendations

### Immediate Actions:
1. **Weight V14 and V12 heavily** in fraud scoring algorithms
2. **Increase monitoring during peak hours** (especially 11 AM)
3. **Implement amount category rules** based on V1 patterns

### Model Improvements:
1. **Address class imbalance** with SMOTE or ensemble methods
2. **Test alternative algorithms** (Random Forest, XGBoost)
3. **Feature engineering** combining time, amount, and PCA components

### Business Implementation:
1. **Two-tier alert system** to reduce false positives
2. **Real-time monitoring** focusing on high-risk combinations
3. **Regular model retraining** to adapt to new fraud patterns

---

## 📁 Dataset Features
| Feature | Description |
|---------|-------------|
| Time | Seconds since first transaction |
| Amount | Transaction amount in Euros |
| V1-V28 | PCA-transformed features (anonymized) |
| Class | Target: 0 = Legitimate, 1 = Fraud |

---

## 🎯 Conclusion
This analysis demonstrates that while **fraud detection is challenging** due to class imbalance, **meaningful patterns exist**. The combination of **PCA components (especially V14 and V12) with temporal analysis** provides a solid foundation for fraud detection systems. Future work should focus on **improving precision** while maintaining high recall rates.

---
*Last Updated: Analysis based on 284,807 transactions from European cardholders*
