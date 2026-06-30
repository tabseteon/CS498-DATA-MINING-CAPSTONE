# TASK4 : Dish-Specific Restaurant Ranking
### In this task, we will use the curated dish list from Task 3 to rank restaurants for specific dishes within a cuisine. The goal is not simply to find highly rated restaurants overall, but to identify restaurants with strong dish-specific evidence in review text.

## Method A: Ratings-only baseline 
#### Assumption: Reviews that mention a dish reflect sentiment about that dish. Use the review's overall star rating as a proxy for dish-specific sentiment. 
#### The ratings-only baseline ranks restaurants using review stars from reviews that mention the dish. This is simple and transparent, but it is not dish-specific sentiment.

## Method B: Lexicon-based sentiment 
#### Assumption: Sentiment is detectable from positive and negative word counts in the local context around the dish mention. 
#### Lexicon sentiment scores the sentence/window around the dish mention using positive and negative word lists. This is still simple and interpretable, but it can distinguish cases where the review rating is high while the dish sentence is negative, or vice versa.
#### In Task 4, lexicon sentiment is applied to dish-local evidence windows rather than entire reviews, so students can ask whether the specific sentence around a dish sounds favorable or unfavorable. This creates a more targeted ranking signal than overall review stars while remaining interpretable.
#### Lexicon sentiment is useful because students can inspect why a sentence received a score. It also has predictable weaknesses: sarcasm, negation, domain-specific food language, and short context windows can mislead dictionary-based scoring.
### VADER/TextBlob Lexicon Sentiment

## Method C: Transformer sentiment (RoBERTa)
#### Assumption: Sentiment is detectable from positive and negative word counts in the local context around the dish mention. 
#### We use cardiffnlp/twitter-roberta-base-sentiment as the default transformer sentiment model. This RoBERTa model was fine-tuned on 58 M tweets, making it a reasonable match for Yelp review language: short, informal, opinionated sentences with food and experience vocabulary.
#### The model outputs three classes: LABEL_0 (negative), LABEL_1 (neutral), LABEL_2 (positive). We map maps these to the −1 … +1 scale used by the other methods.
