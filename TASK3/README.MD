# TASK3
### The goal of this task is to mine the data set to discover the common/popular dishes of a particular cuisine. For this task, we would like to identify the dishes that are available for a cuisine by building a dish recognizer.
### The curated dish list you produce here (final_dish_list.csv) is the direct input to Task 4 (Restaurant Ranking). Task 4 uses your dish vocabulary to find mentions in reviews, extract local sentiment evidence, and rank restaurants for specific dishes. The quality of Task 4's rankings depends entirely on the quality of Task 3's curation.

# Task 3.1: Mining Dish Names

## N-gram threshold
#### A transparent lexical method that counts how often contiguous word sequences (for example, unigrams, bigrams, and trigrams) appear in review text.
## Modern candidate generation: KeyBERT
#### Extract keyphrases from documents using sentence embeddings.

## Classical vs. modern comparison:

#### N-gram threshold surfaces high-frequency, corpus-wide patterns. A dish that appears 200 times scores high regardless of document context.
#### KeyBERT surfaces document-representative phrases. A signature dish that characterizes specific restaurants may appear even if its corpus-level frequency is too low for the n-gram threshold.
#### Phrases unique to one business (a signature dish) may appear in KeyBERT results but not in n-gram candidates because their global count is below MIN_DF.

# Task 3.2: Manual seed lists and curation setup
## Manual seed lists
#### Seed Dishes: Seed Dishes consist of highly specific standalone menu items rather than generic terms to precisely anchor the target Mexican cuisine. 

#### Non-Dish Terms: Non-Dish Terms explicitly define domain-specific noise, such as ingredients, condiments, or sides, that appear food-like but do not constitute a standalone dish.

#### Dish Fragments: Dish Fragments identify single-token components that are too generic on their own but serve as powerful triggers to capture longer, valid compound phrases.

## Curation setup

#### APPROVED_AFTER_REVIEW_DISHES: The specific, compound Mexican dish names that are identifiable as menu items within the review contexts. These valid dishes will significantly improve the data quality for downstream restaurant ranking and sentiment analysis. 

#### REJECTED_OR_REVIEW_ONLY: The non-dish noise is filtered out, including service, price, and ambience descriptors, as well as simple emotional adjectives that do not represent food. Furthermore, single ingredient fragments and overly broad category terms were excluded to refine the Mexican dish data. 



