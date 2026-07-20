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

## 1. The Baseline
## 2. Text-Only Classifier
## 3. Text + Metadata Model
## 4. Advanced Representation
## 5. Evaluation Framework 
## 6. Leakage Audit

#### 
