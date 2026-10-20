# Wine Quality Prediction Using Machine Learning 🍷

A supervised machine learning project that predicts wine quality scores from physicochemical properties using the UCI Wine Quality dataset. This project explores red and white wine separately, performs exploratory data analysis, trains Random Forest regression models, and evaluates the effect of hyperparameter tuning.

## 📌 Project Overview

Wine quality assessment traditionally involves human sensory evaluation. This project investigates whether measurable chemical properties can help predict expert-assigned wine quality scores.

The project is based on the dataset and research paper by Cortez et al. (2009), with an additional implementation of Random Forest regression.

**Project type:** Supervised Machine Learning — Regression

## 🎯 Objectives

- Explore the physicochemical properties of red and white wine.
- Investigate correlations between chemical features and quality scores.
- Train separate Random Forest regression models for red and white wine.
- Evaluate model performance using MAE, RMSE, and R².
- Experiment with Random Forest hyperparameters using `RandomizedSearchCV` and cross-validation.
- Compare the original and tuned model configurations.

## 📚 Research Paper

**Title:** Modeling Wine Preferences by Data Mining from Physicochemical Properties

**Authors:** Paulo Cortez, António Cerdeira, Fernando Almeida, Telmo Matos, and José Reis

**Published in:** Decision Support Systems, Volume 47, Issue 4, 2009, pages 547–553.

- [Read the paper — DOI link](https://doi.org/10.1016/j.dss.2009.05.016)
- [Read the available preprint PDF](https://www3.dsi.uminho.pt/pcortez/winequality09.pdf)

The original study investigates regression techniques, including multiple regression, neural networks, and support vector machines, for predicting wine quality from physicochemical measurements.

This repository uses the same dataset for a learning-oriented implementation of Random Forest regression. It is inspired by the published study but is **not a complete reproduction of the original experimental methodology**.

## 📊 Dataset

**Source:** [UCI Machine Learning Repository — Wine Quality](https://archive.ics.uci.edu/dataset/186/wine+quality)

**Dataset DOI:** [10.24432/C56S3T](https://doi.org/10.24432/C56S3T)

The dataset contains Portuguese Vinho Verde wine samples, with separate files for red and white wine.

| Dataset | Number of samples | Columns |
|---|---:|---:|
| White wine | 4,898 | 12 |
| Red wine | 1,599 | 12 |

Each dataset contains 11 physicochemical input features and one target variable, `quality`.

### Features

- Fixed acidity
- Volatile acidity
- Citric acid
- Residual sugar
- Chlorides
- Free sulfur dioxide
- Total sulfur dioxide
- Density
- pH
- Sulphates
- Alcohol

**Target:** `quality` — the expert-assigned wine quality score.

The quality scores in these datasets range from 3 to 9.

## 🛠️ Tech Stack

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook

## ⚙️ Methodology

### 1. Data loading and inspection
Load the CSV files and inspect their dimensions, data types, missing values, and target distributions.

### 2. Exploratory Data Analysis
- Analyze the distribution of wine quality scores.
- Generate correlation heatmaps.
- Investigate relationships between alcohol content and quality.
- Examine feature distributions and potential outliers.

### 3. Train-test split
Use an 80:20 train-test split with `random_state=42` for the initial experiments.

### 4. Model training
Train a Random Forest regressor using physicochemical properties to predict quality scores.

### 5. Model evaluation
Evaluate predictions using:

- **Mean Absolute Error (MAE):** Average absolute prediction error.
- **Root Mean Squared Error (RMSE):** Error metric that penalizes larger errors more heavily.
- **R² Score:** Measures predictive performance relative to predicting the mean target value.

### 6. Hyperparameter tuning
Use `RandomizedSearchCV` with five-fold cross-validation to explore different combinations of:

- Number of trees (`n_estimators`)
- Maximum tree depth (`max_depth`)
- Minimum samples required to split a node (`min_samples_split`)
- Minimum samples per leaf (`min_samples_leaf`)
- Number of features considered at each split (`max_features`)

The tuning procedure selects a configuration based on cross-validation MAE. The selected model is then evaluated on the held-out test set.

## 📈 Results

The initial white wine Random Forest experiment used 300 trees and produced the following results on the test set:

| Metric | White wine — Random Forest |
|---|---:|
| MAE | 0.4167 |
| RMSE | 0.5876 |
| R² | 0.5542 |

These results are from the initial experiment. The 500-tree configuration also showed a small improvement during the tree-count comparison.

Hyperparameter tuning did not improve the white wine test-set results in the configuration tested.

Red wine was evaluated separately. Its original Random Forest configuration performed better than its tuned configuration on the test set in the experiments conducted.

*Note: The final red wine metrics and final selected configurations should be recorded from the notebook before publishing a complete numerical comparison.*

## 🔍 Key Observations

- Alcohol showed a positive correlation with white wine quality in the exploratory analysis.
- Density showed a negative correlation with white wine quality.
- Residual sugar and density were strongly positively correlated in the white wine dataset.
- Increasing the number of trees from 100 to 500 produced only a small improvement in test-set performance.
- Hyperparameter tuning did not guarantee improved generalization.

These observations describe associations and predictive results; they do not establish causal relationships between chemical properties and wine quality.

## 📁 Repository Structure

```text
wine-quality-prediction-ml/
├── main.ipynb
├── winequality-red.csv
├── winequality-white.csv
├── winequality.names
└── README.md
```

## 🚀 How to Run

1. Clone this repository:

   ```bash
   git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
   ```

2. Navigate to the project directory:

   ```bash
   cd YOUR_REPOSITORY
   ```

3. Install the required libraries:

   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter
   ```

4. Start Jupyter Notebook:

   ```bash
   jupyter notebook
   ```

5. Open `main.ipynb` and run the cells sequentially.

Ensure that both CSV files are in the same directory as the notebook, or update their file paths accordingly.

## ⚠️ Limitations

- The dataset contains a limited number of samples, particularly for some extreme quality scores.
- The model predicts expert-assigned quality scores, not an objective or universally agreed measure of taste.
- Random train-test splits can produce different results with different seeds.
- Hyperparameter selection can overfit the validation procedure if too many configurations are explored.
- The experiments in this repository do not fully reproduce the original paper's model-selection procedure.

## 🔮 Future Improvements

- Implement Linear Regression and Support Vector Regression.
- Compare models using consistent validation and test procedures.
- Investigate feature selection and feature importance.
- Use repeated cross-validation to assess performance variability.
- Compare separate red and white models with a combined model that includes wine type as a feature.
- Add a simple prediction interface for new wine measurements.

## 📖 References

Cortez, P., Cerdeira, A., Almeida, F., Matos, T., & Reis, J. (2009). Modeling wine preferences by data mining from physicochemical properties. *Decision Support Systems, 47*(4), 547–553. https://doi.org/10.1016/j.dss.2009.05.016

Cortez, P., Cerdeira, A., Almeida, F., Matos, T., & Reis, J. (2009). *Wine Quality Dataset*. UCI Machine Learning Repository. https://doi.org/10.24432/C56S3T

## 📜 Dataset License

The UCI repository lists the dataset under the **CC BY 4.0** license. Please retain the dataset attribution and follow the license terms when redistributing the data.

---

**If you find this project useful, feel free to star the repository!**
