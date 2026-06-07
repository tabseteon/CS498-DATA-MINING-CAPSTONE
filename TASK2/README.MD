# Task2
## The goal of this task is to mine the data set to construct a cuisine map to visually understand the landscape of different types of cuisines and their similarities. The cuisine map can help users understand what cuisines are available and their relations, which allows for the discovery of new cuisines, thus facilitating exploration of unfamiliar cuisines.

# Task 2.1: Visualization of the Cuisine Map
## Implemented Models
### 1. TF-IDF
### 2. Embedding Model (BERTopic)

# Task 2.2: Improving Cuisine Maps
## 1) Varying the text representation - TF-IDF Weighted Sentence Embedding
### Instead of using a naive mean computation, we dynamically compute a weighted average of all-MiniLM-L6-v2 dense embeddings using token-level global TF-IDF scores

## 2) Varying the similarity function - Min-Max Scaling

# Task 2.3: Incorporating Clustering Cuisine Maps
## Implemented Models
### 1. HDBSCAN Density Clustering (Noise-Aware)
### 2. K-Means Partitioning ($K=3$ vs $K=5$)
