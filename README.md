## Learn KNN: Penguins Species Classification

This repository contains a Jupyter Notebook (`knn-learn.ipynb`) that walks through building a basic k-Nearest Neighbors (KNN) classifier to predict penguin species using the Palmer Penguins dataset (via `seaborn`). It is designed as a learning exercise for fundamental machine learning workflow concepts: data loading, cleaning, feature selection, scaling, model training, and evaluation.

### 1. Dataset

We use the Palmer Penguins dataset, which includes physical measurements of penguins from three species: Adelie, Chinstrap, and Gentoo. Selected numeric features:
- `bill_length_mm`
- `bill_depth_mm`
- `flipper_length_mm`
- `body_mass_g`

Target: `species`.

### 2. Data Cleaning

Rows containing missing values are dropped for simplicity (`dropna()`). This is an intentional simplification for a first pass. In a more robust pipeline, you might:
- Impute (mean/median or model-based)
- Analyze whether missingness is systematic
- Avoid discarding valuable data points

### 3. Feature / Target Separation

`X` holds the numeric features; `y` holds the species labels. Understanding this separation is key for scikit-learn estimators.

### 4. Train / Test Split

We use `train_test_split` with `stratify=y` to preserve class balance in both sets. Test size = 30%. Stratification helps avoid skewed evaluation when classes differ in frequency.

### 5. Scaling

KNN relies on distance metrics (typically Euclidean). Features measured on different scales can distort those distances. We apply `StandardScaler` (z-score normalization) to ensure each feature contributes comparably.

### 6. Model Training (KNN)

Instantiate: `KNeighborsClassifier(n_neighbors=5)`.
Fit: `knn.fit(X_train_scaled, y_train)`.
Prediction: `y_pred = knn.predict(X_test_scaled)`.

Why k=5? It's a reasonable starting default. In practice, tune `k` via cross-validation (e.g., try a range like 1–25 and select the value maximizing validation accuracy while avoiding overfitting).

### 7. Evaluation Metrics

The notebook prints:
- **Accuracy**: Overall proportion of correct predictions.
- **Classification Report**: Precision, recall, f1-score per class.
- **Confusion Matrix (heatmap)**: Counts of actual vs. predicted classes for visual diagnostics.

Interpreting the confusion matrix helps identify which species the model confuses (e.g., similar morphology between Adelie and Chinstrap could lead to misclassifications).

### 8. Why Scaling Matters for KNN

Without scaling, features with larger numeric ranges (like body mass) dominate the distance computation and can bias neighbor selection. Standardizing centers features at mean 0, variance 1, reducing scale-driven bias.
