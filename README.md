# Colon Cancer Gene Expression Analysis

Feature Selection, Dimensionality Reduction & Classification

A comparative machine learning study of feature selection, dimensionality reduction, and classification methods applied to high-dimensional colon tumor gene expression data.

The project investigates how different feature-selection strategies perform in a high-dimensional, low-sample-size (HDLSS) setting and explores whether combining multiple selection methods can produce more compact and consistent feature representations.

---

## Overview

Gene expression datasets often contain thousands of features while having a relatively small number of biological samples. This creates challenges for machine learning, including high dimensionality, overfitting, and feature redundancy.

This project compares multiple feature-selection approaches and evaluates their impact on downstream classification performance. The analysis includes:

- Filter-based feature selection
- Wrapper-based feature selection
- Embedded feature selection
- Dimensionality reduction using PCA
- Consensus and feature-overlap analysis
- Multiple machine learning classifiers
- Sequential Backward Elimination
- Genetic Algorithm-based feature selection
- Attention-based neural network experiments

---

## Dataset

The project uses the Colon Tumor gene expression dataset, originally introduced by Alon et al.

**Characteristics:**

- 62 samples
- 2,000 gene-expression features
- 40 tumor samples
- 22 normal samples

The dataset represents a typical high-dimensional, low-sample-size classification problem, where the number of features is substantially larger than the number of observations.

> The raw dataset is not included in this repository. See [`data/README.md`](data/README.md) for dataset provenance and instructions for obtaining the data.

---

## Methodology

The overall workflow consists of preprocessing, feature selection, dimensionality reduction, classification, and comparative analysis.

### 1. Preprocessing

- Data preparation
- Stratified 5-fold cross-validation
- Standardization
- Class balancing using SMOTE (`k_neighbors=3`)
- Preprocessing applied within the cross-validation workflow to prevent data leakage

### 2. Feature Selection

Nine feature-selection methods are evaluated across three methodological families.

**Filter methods**
- ANOVA F-test
- Mutual Information

**Wrapper methods**
- RFE with SVM
- RFE with Logistic Regression
- Boruta

**Embedded methods**
- LASSO
- Elastic Net
- Random Forest
- XGBoost

Selected feature sets are compared to investigate feature stability and overlap across approaches.

### 3. Classification

Selected features are evaluated using the following classifiers:

- K-Nearest Neighbors (KNN)
- Support Vector Machine (SVM)
- Naive Bayes
- Decision Tree
- Random Forest
- Logistic Regression

Performance is evaluated using Balanced Accuracy, F1 Score, and ROC-AUC.

---

## Consensus Feature Analysis

Beyond evaluating individual feature-selection methods, the project investigates overlap between selected features:

- Feature overlap between selection methods
- Cross-family consensus
- Features repeatedly selected by different methods
- Compact feature subsets derived from the intersection of multiple approaches

This examines whether certain features remain important across different feature-selection strategies rather than relying on a single method.

---

## Dimensionality Reduction

Principal Component Analysis (PCA) is used to investigate the structure of the gene-expression data and reduce dimensionality. PCA also serves as a validation step for the feature-selection analysis, relating selected feature subsets to the main sources of variance in the dataset.

---

## Advanced Experiments

- Sequential Backward Elimination (SBE)
- Genetic Algorithm (GA)
- Attention-gated Artificial Neural Network
- GA + ANN experiments

---

## Experimental Design

The main evaluation uses 5-fold stratified cross-validation. To reduce the risk of information leakage, scaling and SMOTE are applied within the cross-validation workflow rather than before the folds are created. Feature-selection methods are compared using the same evaluation framework.

---

## Project Structure

```text
colon-cancer-gene-expression-analysis/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   └── README.md
│
└── notebook
```

---

## Installation

```bash
git clone https://github.com/YOUR_USERNAME/colon-cancer-gene-expression-analysis.git
cd colon-cancer-gene-expression-analysis

python -m venv venv

# Windows
venv\Scripts\activate

# macOS/Linux
source venv/bin/activate

pip install -r requirements.txt
```

---

## Running the Project

The main analysis is provided as a Jupyter notebook:

```text
notebooks/dami2projectfinal.ipynb
```

Obtain the dataset per the instructions in [`data/README.md`](data/README.md) before running the notebook. The dataset path may need to be updated depending on your local environment.

---

## Limitations

- The dataset contains only 62 samples.
- The number of gene-expression features is much larger than the number of samples.
- The small sample size creates a substantial risk of overfitting.
- Feature-selection results may vary depending on method and experimental setup.
- Selected features should be interpreted as statistical or model-based indicators rather than definitive biological biomarkers.
- No independent external validation dataset was used.

Results should be considered exploratory rather than definitive clinical or biological conclusions.

---

## References

The dataset originates from the work of Alon et al. on gene expression profiles of colon cancer. Additional methodological references are provided in the project notebook.
