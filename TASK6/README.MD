# TASK6 : Future Restaurant Quality-Decline Prediction
### In this task, we build a supervised learning pipeline to predict whether a restaurant is at risk of future quality decline based on its historical Yelp review evidence. 
### This task uses Yelp review and business data directly. Reviews before a cutoff date are used to create historical features, and reviews after the cutoff date are used to define the future risk label.
### The main challenge is to design a prediction task that is both useful and leakage-safe. A model should only use information that would have been available before the cutoff date. You will compare multiple feature and model strategies, such as metadata-only models, text-only models, and combined text-plus-metadata models. Since future decline is usually an imbalanced prediction problem, you will evaluate models using macro-F1 rather than relying only on accuracy.
### The goal is not only to find the highest-scoring model, but to understand what historical Yelp signals can and cannot tell us about future restaurant decline.

## Label Definition: What is "Risk"
#### Risk = 1 when BOTH conditions hold:
##### Quality decline ≥ 0.75 stars: Historical average minus future average ≥ threshold
##### Future average ≤ 3.5 stars: The future quality is objectively low

## Cross-Validation and Viability Constraints
#### To perform cross-validation with imbalanced classes, we need:
#### MIN_POSITIVE_EXAMPLES = 25 : At least 25 risk=1 businesses across the entire dataset
#### MIN_CLASS_RATE = 10% : The minority class must be at least 10% of the data
#### MIN_EXAMPLES_PER_CV_FOLD = 5 : Each fold must have at least 5 examples per class

## Build the Future Quality-Decline Prediction Frame
#### Convert Yelp reviews into a supervised learning problem
#### 1. Split reviews by cutoff date → historical window (features) vs future window (labels)
#### 2. Aggregate by business → historical average stars, historical review counts, historical sentiment, and historical text
#### 3. Compute labels → risk=1 if future quality declines enough and the future average is low enough


## Feature Groups and Models
#### Five feature/model configurations were evaluated with stratified 3-fold cross-validation, all using logistic regression as the classifier so that differences in score reflect the feature representation
## 1. Dummy Baseline: Most-frequent-class predictor.
## 2. M1: Metadata only. (Historical review count, historical average stars, historical lexicon-based sentiment, and historical low-star share)
## 3. M2: TF-IDF only. (TF-IDF vectorized historical review text, no structured features)
## 4. M3 – TF-IDF + metadata. (TF-IDF text combined with the M1 structured features via a ColumnTransformer)
## 5. M4 – LSA + metadata (TF-IDF text compressed with Truncated SVD (latent semantic analysis) and combined with the M1 structured features)
## 6. ST_Logistic Model: Historical review text was also encoded with a pretrained sentence-transformer (all-MiniLM-L6-v2) and fed into logistic regression (ST_Logistic), to test whether dense semantic embeddings outperform sparse TF-IDF for this task.
####  Comparing M3 (sparse TF-IDF) and M4 (compressed LSA) under the same leakage-safe framework reveals whether dimensionality reduction helps or hurts for this prediction task

#### Logistic regression: A linear supervised classifier, providing an interpretable baseline for predicting future restaurant risk from historical text and metadata

## Three technical responses to class imbalance
#### Macro-F1
#### Stratified K-fold cross-validation: Split labeled examples into folds while preserving class proportions as much as possible. This is crucial because risk/pass labels can be imbalanced and the labeled sample is small.
#### Class weighting in model training: Most sklearn classifiers support class_weight="balanced", up-weighting the loss for minority-class errors during training.
