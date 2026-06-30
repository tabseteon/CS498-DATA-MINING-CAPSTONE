# TASK5 : Temporal Evidence Mining
### Task 5 adds a time dimension to the restaurant review project. In this task, we will detect temporal patterns in dish popularity, sentiment trends, and review language change.

## Configuration Choices 
#### TIME_GRANULARITY: QUARTER
##### Quarter is the recommended default for Yelp data because monthly bins are often too sparse (< 20 reviews) for most businesses, and yearly bins smooth over real intra-year variation.
#### MIN_REVIEWS_PER_TIME_BIN: 20
##### A bin with 5 reviews produces unreliable means; a bin with 20+ reviews gives you something defensible.
#### MAX_BUSINESSES and MAX_REVIEWS_TOTAL: 80 and 10000
##### Both caps must be consistent. If you raise MAX_BUSINESSES to 200 but keep MAX_REVIEWS_TOTAL at 10,000, each business gets roughly 50 reviews on average which is not enough for per-business trends.
#### MAX_DISHES: 4
##### Tracking too many dishes at once makes the heatmaps unreadable and the analysis unfocused. Twelve dishes is a reasonable upper bound. We will probably focus on three to five.

## Construct the temporal review subset
#### We join reviews to business metadata, parse dates, assign time bins, and drop under-supported time bins.
#### The minimum time-bin threshold is important: a visual trend based on a tiny number of reviews is usually not reliable.

## Method A: Temporal TF-IDF Shift Analysis
#### This method compares which terms are distinctive in different time bins. We aggregate review text by period, vectorize each period, and inspect changing top terms or heatmaps to understand how review language evolves. This is a classical text-mining method measuring changes in individual term frequencies.

## Method B: Temporal Embedding Drift Analysis
#### Embedding-centroid drift measures shifts in overall meaning: a large centroid distance between two bins suggests the topics, tone, and vocabulary changed substantially.
#### We encode each time-bin's reviews into a centroid embedding (using sentence-transformers or a TF-IDF + SVD fallback), then measure cosine distance between consecutive bin centroids.
