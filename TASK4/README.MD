# TASK4 : Dish-Specific Restaurant Ranking
### In this task, we will use the curated dish list from Task 3 to rank restaurants for specific dishes within a cuisine. The goal is not simply to find highly rated restaurants overall, but to identify restaurants with strong dish-specific evidence in review text.

## N-gram threshold
#### A transparent lexical method that counts how often contiguous word sequences (for example, unigrams, bigrams, and trigrams) appear in review text.
## Method C — Transformer sentiment (RoBERTa)
#### Assumption: Sentiment is detectable from positive and negative word counts in the local context around the dish mention. 
#### We use cardiffnlp/twitter-roberta-base-sentiment as the default transformer sentiment model. This RoBERTa model was fine-tuned on 58 M tweets, making it a reasonable match for Yelp review language: short, informal, opinionated sentences with food and experience vocabulary.
#### The model outputs three classes: LABEL_0 (negative), LABEL_1 (neutral), LABEL_2 (positive). We map maps these to the −1 … +1 scale used by the other methods.
