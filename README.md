# Comparative Machine Learning Analysis Across Time-Series, Tabular, and Image Data

This repository contains a multi-dataset machine learning project that applies supervised learning techniques to **three fundamentally different data modalities**:  
- Time-series data  
- Tabular demographic data  
- Image data

 SignalSavants_Dataset1.ipynb`  
  **Time-Series Regression on Daily Minimum Temperatures**  
  Feature-based regression using lag variables and rolling statistics to predict daily minimum temperature values.

- `SignalSavants_Dataset2.ipynb`  
  **Tabular Classification on Adult Income Data**  
  Supervised classification using demographic and socioeconomic features to predict income category.

- `SignalSavants_Dataset3.ipynb`  
  **Image Classification on MNIST Handwritten Digits**  
  Multiclass classification of handwritten digits using flattened pixel features and dimensionality-aware modeling.

- `daily-min-temperatures.csv`
- `adult_clean.csv`
- `mnist_clean.csv`

A **consistent and principled machine learning pipeline** is maintained across all datasets, emphasizing correct data handling, justified model selection, rigorous evaluation, and ethical awareness.

---

## Overall Project Goal

The objective of this project is to demonstrate how machine learning methodologies must adapt to different data structures while preserving sound experimental design.

Each dataset notebook is structured as a **technical narrative**, not a code dump, and includes:

- Purpose-driven data exploration  
- Preprocessing and feature reasoning  
- Model selection with justification  
- Evaluation and comparative analysis  
- Ethical considerations  

---

## Dataset 1: Daily Minimum Temperatures  
**Task:** Time-Series Regression

### Data Exploration
Initial exploration focused on understanding temporal structure and data integrity:
- Verified a single continuous target variable (daily temperature)
- Confirmed absence of missing values
- Converted date column to datetime format and sorted chronologically

**Goal:**  
Determine whether temporal dependence exists and whether standard regression methods are applicable.

### Key Observations
- Smooth, continuous temperature signal  
- Clear seasonal and temporal dependence  
- No extreme outliers or regime shifts  
- Strong autocorrelation across time  

---

### Feature Engineering (Time-Series Specific)
To account for temporal dependence, the following features were constructed:
- Lagged temperature values
- Rolling averages (7-day mean)

**Justification:**  
Time-series data violates the i.i.d. assumption. Lag-based features convert the problem into a supervised learning setting without leaking future information.

---

### Train/Test Strategy
- Chronological split (no shuffling)
- Training data strictly precedes test data in time

This preserves causality and prevents data leakage.

---

### Models Used
**Linear Regression**
- Baseline model
- Suitable for smooth, continuous signals
- Assumes linear relationships between lagged features

**Random Forest Regression**
- Evaluates whether nonlinear interactions improve performance
- Automatically captures feature interactions

---

### Results & Interpretation
- Linear Regression slightly outperformed Random Forest
- Indicates the underlying process is largely linear
- Random Forest added complexity without meaningful performance gains

**Conclusion:**  
For smooth, seasonal time-series data with strong autocorrelation, simpler linear models can outperform more complex nonlinear approaches.

---

### Ethics Discussion
Although the dataset does not involve human subjects:
- Over-reliance on forecasts can impact agriculture, infrastructure, and energy planning
- Model uncertainty should be communicated clearly
- Predictions should not be treated as deterministic outcomes

---

## Dataset 2: Adult Income Dataset  
**Task:** Tabular Binary Classification

### Data Exploration
Exploration focused on:
- Dataset dimensionality
- Feature types (categorical vs. numerical)
- Income class distribution
- Missing value inspection

**Goal:**  
Understand feature structure and class balance before model selection.

---

### Key Observations
- Mixed categorical and numerical features
- Moderate class imbalance
- No severe missing data after cleaning
- Features represent real socioeconomic attributes

---

### Preprocessing & Feature Reasoning
- Categorical features encoded numerically
- No artificial feature creation without justification
- Original feature set retained because:
  - Each feature has clear semantic meaning
  - No extreme multicollinearity observed

**Rationale:**  
For tabular data, interpretability and semantic clarity are prioritized over aggressive feature engineering.

---

### Train/Test Strategy
- Proper train/test split
- Preprocessing applied *after* splitting to avoid leakage
- Evaluation emphasized class-level metrics, not just accuracy

---

### Models Used
**Logistic Regression**
- Interpretable linear classifier
- Strong baseline for tabular binary classification
- Assumes linear decision boundary

**Random Forest Classifier**
- Nonparametric ensemble method
- Captures nonlinear feature interactions
- Less sensitive to feature scaling

---

### Comparative Analysis
- Random Forest achieved higher overall accuracy
- Logistic Regression performed competitively on majority classes
- Random Forest better handled nonlinear relationships and minority classes

**Conclusion:**  
When relationships between features and outcomes are nonlinear, ensemble methods outperform linear classifiers.

---

### Ethics Discussion
This dataset raises important ethical concerns:
- Risk of reinforcing socioeconomic bias
- Potential misuse in automated decision-making (e.g., hiring, lending)
- Need for transparency, fairness, and human oversight

Models are treated as analytical tools, not decision authorities.

---

## Dataset 3: MNIST Handwritten Digits  
**Task:** Image Classification

### Data Exploration
Initial steps included:
- Verifying dataset shape and label distribution
- Confirming normalized pixel values
- Attempting image reconstruction and diagnosing reshape errors

**Key Insight:**  
Images are stored as **flattened feature vectors**, not raw 2D images.

---

### Feature Understanding
Each sample:
- Contains 784 features (28 × 28 pixels flattened)
- Pixel values represent grayscale intensity

Rather than reshaping arbitrarily, the flattened representation was treated as a **high-dimensional feature space**.

---

### Visualization
- Plotted flattened feature vectors
- Examined pixel intensity distributions
- Image reconstruction used only for interpretability

---

### Models Used
**Multiclass Logistic Regression**
- Strong baseline for high-dimensional linear classification
- Efficient and interpretable
- Uses one-vs-rest strategy internally

**Random Forest Classifier**
- Captures nonlinear pixel interactions
- Higher computational cost but increased flexibility

---

### Results & Interpretation
- Logistic Regression achieved strong performance despite simplicity
- Random Forest slightly improved accuracy at higher cost
- Certain digits (e.g., 0, 1) were easier to classify than visually similar digits (e.g., 3 vs. 5)

**Conclusion:**  
High-dimensional image data can often be effectively classified using linear models when features are well-structured.

---

### Ethics Discussion
- Handwritten digit recognition is low-risk
- Similar techniques applied to facial recognition or surveillance raise privacy concerns
- Ethical deployment depends on domain, not just accuracy

---

## Cross-Dataset Comparative Insights

Across all three datasets:
- Model choice was guided by data structure, not convenience
- Simpler models often performed competitively
- Proper data splitting prevented overfitting and leakage
- Interpretability was prioritized when appropriate

---

## Final Takeaway

This project demonstrates that **effective machine learning is not about maximizing accuracy**, but about:
- Understanding data characteristics
- Matching model assumptions to data structure
- Making defensible methodological choices
- Evaluating results critically and ethically
