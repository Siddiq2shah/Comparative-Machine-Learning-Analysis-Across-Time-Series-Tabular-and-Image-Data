# Comparative-Machine-Learning-Analysis-Across-Time-Series-Tabular-and-Image-Data
This repository contains a multi-dataset machine learning project developed.   The project applies supervised learning methods to three fundamentally different data modalities—time-series data, tabular demographic data, and image data, using a consistent, principled machine learning pipeline.


**Overall Project Goal**

The goal of this project was to apply supervised machine learning methods to three fundamentally different types of data—time-series, tabular, and image data—while maintaining a principled, consistent ML pipeline across datasets.

For each dataset, the notebook is structured as a technical narrative, not a code dump:

Data exploration with a clear purpose

Preprocessing and feature reasoning

Model selection and justification

Evaluation and comparative analysis

Ethical considerations

Dataset 1: Daily Minimum Temperatures (Time-Series Regression)
Data Exploration

I began by inspecting the structure of the dataset:

Confirmed the dataset contains one continuous target variable (temperature) recorded daily

Verified there were no missing values

Converted the date column into a proper datetime format and sorted chronologically

Purpose of exploration:
To understand whether the data is suitable for standard regression and whether temporal structure exists.

Key Observations

The temperature signal is smooth and continuous

Clear seasonal and temporal dependence

No abrupt regime shifts or extreme outliers

Strong evidence that past values influence future values

Feature Engineering (Time-Series Specific)

Because standard regression models do not inherently understand time, I explicitly encoded temporal dependence using:

Lag features (previous day temperatures)

Rolling averages (7-day mean)

Why this is justified:
Time-series data violates the i.i.d. assumption. Creating lagged features converts the problem into a supervised learning task without leaking future information.

Train/Test Strategy

No shuffling

Chronological split to prevent data leakage

Training data precedes test data in time

This preserves causality and avoids artificially inflated performance.

Models Used
Linear Regression

Chosen as a baseline due to the smooth, continuous nature of the signal

Assumes linear relationships between lagged values and future temperature

Random Forest Regression

Chosen to test whether nonlinear relationships provide improvement

Can capture interactions between lag features without manual specification

Results & Interpretation

Linear Regression slightly outperformed Random Forest

Indicates the underlying process is largely linear

Random Forest introduced unnecessary complexity without performance gain

Conclusion:
For smooth, seasonal time-series with strong autocorrelation, simple linear models can outperform more complex nonlinear models.

Ethics Discussion

Although this dataset does not involve human subjects:

Over-reliance on temperature forecasts can impact agriculture, infrastructure, and energy planning

Model uncertainty should be communicated

Predictions should not be treated as deterministic truth

Dataset 2: Adult Income Dataset (Tabular Classification)
Data Exploration

Initial exploration focused on:

Dataset dimensionality

Feature types (categorical vs numerical)

Class distribution of income labels

Missing value inspection

Purpose:
To understand feature structure and class balance before selecting a classifier.

Key Observations

Mixed feature types

Moderate class imbalance

No severe missing data after cleaning

Features represent real demographic and socioeconomic attributes

Preprocessing & Feature Reasoning

Categorical features encoded numerically

No artificial feature creation without justification

Feature set retained because:

Each feature has a clear semantic meaning

No extreme multicollinearity observed that warranted removal

Rationale:
In tabular data, feature interpretability matters more than aggressive feature engineering.

Train/Test Strategy

Proper train/test split

No preprocessing applied before splitting to avoid leakage

Evaluation focused on class-level metrics, not just accuracy

Models Used
Logistic Regression

Interpretable linear classifier

Suitable baseline for tabular binary classification

Assumes linear decision boundary

Random Forest Classifier

Nonparametric model

Handles nonlinear interactions between features

Less sensitive to feature scaling

Comparative Analysis

Random Forest achieved higher overall accuracy

Logistic Regression performed competitively on majority classes

Random Forest better handled nonlinear relationships and minority classes

Conclusion:
When relationships between demographic features and outcomes are nonlinear, ensemble methods outperform linear classifiers.

Ethics Discussion

This dataset raises real ethical concerns:

Risk of reinforcing socioeconomic bias

Potential misuse in automated decision-making (e.g., lending, hiring)

Importance of transparency and fairness

The model is treated as an analytical tool, not a decision authority.

Dataset 3: MNIST Handwritten Digits (Image Classification)
Data Exploration

Initial steps included:

Verifying dataset shape and label distribution

Confirming pixel values are normalized

Attempting image reconstruction (and diagnosing reshape issues)

Key realization:
The data is stored as flattened vectors, not raw images.

Feature Understanding (Critical Insight)

Each sample:

Contains 784 features (28×28 pixels flattened)

Pixel intensity values represent grayscale brightness

Rather than reshaping arbitrarily, the flattened representation was treated as a high-dimensional feature vector.

Visualization

Plotted flattened feature vectors

Visualized pixel intensity distributions

Used reconstruction only for interpretability, not modeling

Models Used
Logistic Regression (Multiclass)

Strong baseline for high-dimensional linear classification

Efficient and interpretable

Uses one-vs-rest internally

Random Forest Classifier

Captures nonlinear pixel interactions

More flexible but computationally heavier

Results & Interpretation

Logistic Regression achieved strong performance despite simplicity

Random Forest slightly improved accuracy but at higher computational cost

Certain digits (e.g., 1, 0) classified more easily than visually similar digits (e.g., 3 vs 5)

Conclusion:
High-dimensional image data can often be classified effectively using linear models when features are well-structured.

Ethics Discussion

Handwritten digit recognition is low-risk

However, similar models applied to facial recognition or surveillance raise privacy concerns

Ethical deployment depends on domain, not just accuracy

Cross-Dataset Comparative Insights

Across all three datasets:

Model choice was guided by data structure, not convenience

Simpler models often performed competitively

Overfitting was avoided through correct data splitting

Interpretability was prioritized where appropriate
