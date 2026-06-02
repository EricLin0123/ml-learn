Here are the commonly used scikit-learn features:

---

## 1. Supervised Learning

**Classification**

- `LogisticRegression` — Linear model for binary/multiclass classification
- `SVC` (Support Vector Classifier) — Finds optimal hyperplane margin between classes
- `RandomForestClassifier` — Ensemble of decision trees, great for tabular data
- `KNeighborsClassifier` — Classifies based on nearest neighbor votes

**Regression**

- `LinearRegression` — Fits a linear relationship between features and a continuous target
- `Ridge` / `Lasso` — Regularized regression to reduce overfitting
- `GradientBoostingRegressor` — High-accuracy sequential tree boosting

**Ensembles**

- `RandomForest` — Bagging of trees to reduce variance
- `GradientBoostingClassifier` / `HistGradientBoosting` — Boosting for high performance
- `AdaBoostClassifier` — Reweights samples to focus on hard examples
- `VotingClassifier` / `StackingClassifier` — Combines multiple model predictions

---

## 2. Unsupervised Learning

**Clustering**

- `KMeans` — Partitions data into k clusters by centroid distance
- `DBSCAN` — Density-based clustering; handles arbitrary shapes and marks outliers
- `AgglomerativeClustering` — Hierarchical bottom-up clustering

**Dimensionality Reduction**

- `PCA` — Projects data onto principal components; great for preprocessing and visualization
- `TruncatedSVD` — PCA variant for sparse matrices (e.g. TF-IDF text data)
- `t-SNE` — Non-linear 2D/3D visualization of high-dimensional data

**Anomaly Detection**

- `IsolationForest` — Isolates anomalies via random splits
- `LocalOutlierFactor` — Flags points with low local density relative to neighbors
- `OneClassSVM` — Learns a boundary around normal data

---

## 3. Preprocessing

**Scaling**

- `StandardScaler` — Zero mean, unit variance; essential for SVM, PCA, logistic regression
- `MinMaxScaler` — Squeezes features into [0, 1]
- `RobustScaler` — Uses median/IQR; resistant to outliers

**Encoding**

- `OneHotEncoder` — Converts categorical variables to binary indicator columns
- `LabelEncoder` — Maps class labels to integers
- `OrdinalEncoder` — Encodes ordered categories as integers

**Imputation**

- `SimpleImputer` — Fills missing values with mean, median, or a constant
- `KNNImputer` — Fills missing values using k-nearest neighbor similarity
- `IterativeImputer` — Models each feature as a function of the others (MICE-style)

---

## 4. Model Selection & Evaluation

**Validation**

- `train_test_split` — Splits data into train/test sets, with optional stratification
- `KFold` / `StratifiedKFold` — k-fold cross-validation splits
- `cross_val_score` — Evaluates a model across multiple folds in one call

**Hyperparameter Tuning**

- `GridSearchCV` — Exhaustive search over a parameter grid
- `RandomizedSearchCV` — Random sampling of parameter combinations; faster at scale

**Metrics**

- Classification: `accuracy_score`, `f1_score`, `precision_score`, `recall_score`, `roc_auc_score`, `confusion_matrix`
- Regression: `mean_squared_error`, `mean_absolute_error`, `r2_score`
- `classification_report` — Prints precision, recall, F1 per class in one summary

---

## 5. Pipelines & Feature Engineering

- `Pipeline` — Chains transformers and a final estimator; `fit`/`predict` works on the whole chain; prevents data leakage
- `ColumnTransformer` — Applies different transformations to different columns in parallel (e.g. scale numerics, encode categoricals)
- `FunctionTransformer` — Wraps any Python function as a sklearn-compatible transformer
- `SelectKBest` — Selects top k features by a statistical test (e.g. chi², ANOVA F)
- `RFE` (Recursive Feature Elimination) — Prunes features iteratively based on model importance
- `VarianceThreshold` — Removes low-variance (near-constant) features

---

## 6. Utilities

- `joblib.dump` / `joblib.load` — Serialize and reload trained models to disk
- Built-in datasets — `load_iris`, `load_digits`, `make_classification`, `make_regression`, `fetch_openml` for quick experiments
- `clone` — Creates an unfitted copy of an estimator with the same parameters
- `set_config(transform_output="pandas")` — Makes transformers return DataFrames instead of NumPy arrays
