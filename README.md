# Cammeo–Osmancik Rice Classification Model Evaluation

### 📊 Dataset

This dataset contains various characteristics of two rice varieties: Cammeo and Osmancik. It is suitable for developing a machine learning model to predict rice varieties. The dataset contains a total of 3,810 rice grain observations, with features extracted from rice grain images.
<img width="940" height="448" alt="image" src="https://github.com/user-attachments/assets/f79d6abb-7e9c-4f8b-a7ae-adde02ebcf89" />


#### Features

| Variable Name | Type | Description |
|---|---|---|
| Area | Integer | Represents the number of pixels within the boundaries of a rice grain. |
| Perimeter | Continuous | Measures the perimeter of a rice grain by calculating the distance around its boundary. |
| Major_Axis_Length | Continuous | Represents the length of the longest axis of a rice grain. |
| Minor_Axis_Length | Continuous | Represents the length of the shortest axis of a rice grain. |
| Eccentricity | Continuous | Measures the eccentricity of an ellipse with the same moments as the rice grain. |
| Convex_Area | Integer | Represents the number of pixels within the smallest convex hull enclosing the rice grain. |
| Extent | Continuous | Represents the ratio of the area of a rice grain to the area of its bounding box. |

#### Target Variable
- Cammeo
- Osmancik

**Dataset link:** https://archive.ics.uci.edu/dataset/545/rice-cammeo-and-osmancik

(You can find more information about the dataset using the link above.)

## 🤖 Machine Learning Process

### 📊 Exploratory Data Analysis (EDA)

- Most features exhibit relatively well-defined distributions.
<img width="1220" height="746" alt="image" src="https://github.com/user-attachments/assets/718503c7-7d6e-4be8-8510-73474090e38b" />
- Some features contain outliers.
<img width="1351" height="737" alt="image" src="https://github.com/user-attachments/assets/aeee712d-ad9c-4c9a-8a37-557b9b6f3af0" />
- Scatter plots reveal noticeable separation between the two classes.
<img width="805" height="580" alt="image" src="https://github.com/user-attachments/assets/80a29c88-8f2a-4fe0-af75-6b52322c50ed" />
<img width="751" height="563" alt="image" src="https://github.com/user-attachments/assets/32b3961a-55fa-4928-8ae8-9bde6a644b57" />
- Some features are highly correlated.
<img width="817" height="683" alt="image" src="https://github.com/user-attachments/assets/185ffcdd-8b9d-42a2-90b3-589c5da0ebf8" />

*Notebook file: EDA.ipynb*

### 🧰 Preprocessing

- Checked for missing values.
- Checked for duplicate records.
- Split the dataset into training and test sets to prevent data leakage during subsequent processing.

*Notebook file: Preprocessing.ipynb*

### ⚙️ Model Training

**Selected models:**

- Logistic Regression
- Decision Tree
- Random Forest
- Support Vector Machine (SVM)
- K-Nearest Neighbors (KNN)

- Since the dataset contains only 3,810 observations, K-fold cross-validation was used to evaluate model performance.
- GridSearchCV was used for hyperparameter tuning.
- The `Area` and `Convex_Area` features are highly correlated. Therefore, the models were evaluated using three different feature sets to identify the best-performing configuration:
  - **Set 1:** All features
  - **Set 2:** All features except `Area`
  - **Set 3:** All features except `Convex_Area`
- The models were further evaluated by removing outliers and applying techniques such as Forward Feature Selection.

*Notebook files: Model_training_<model_name>.ipynb*

## 📊 Final Model Evaluation

All selected models, with their best hyperparameters and feature sets, were evaluated using unseen test data. The following metrics were used to evaluate model performance:

- Accuracy
- Precision
- Recall
- F1-score

Among the selected models, **Logistic Regression achieved the best overall performance**.
<img width="1253" height="240" alt="image" src="https://github.com/user-attachments/assets/34fbde0f-1db0-48d5-8a76-6e9e16219c0e" />
<img width="1347" height="777" alt="image" src="https://github.com/user-attachments/assets/4044fcb9-018b-4fa2-bfff-0afe26e3e782" />
<img width="1102" height="785" alt="image" src="https://github.com/user-attachments/assets/3cf6e34f-7073-426e-9602-7a898ee88050" />

*Notebook file: Final_model_Evaluation.ipynb*

## ⭐ Feature Importance

The selected final models were evaluated to determine feature importance. Built-in feature importance methods were used for applicable models, along with permutation importance.

Across the different models and techniques, **`Major_Axis_Length` was identified as the most important feature for most models**. In contrast, **Logistic Regression and SVM assigned higher importance to `Convex_Area`**.
<img width="1358" height="785" alt="image" src="https://github.com/user-attachments/assets/e7ded409-1dfc-4db0-91f1-85312733a40e" />
<img width="1126" height="616" alt="image" src="https://github.com/user-attachments/assets/a62fe95d-8e93-4903-8d52-5951defe8972" />
<img width="1123" height="603" alt="image" src="https://github.com/user-attachments/assets/7297416e-e41d-458d-892e-d8fca0e8e88f" />

*Notebook file: Feature_importance.ipynb*
