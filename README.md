# Movie Recommendation System - ReelSense Project

## Overview

This project implements a **hybrid movie recommendation system** that combines **content-based filtering** and **collaborative filtering** to provide personalized movie recommendations. The system also incorporates **diversity, novelty, and explainability**, ensuring that recommendations are not only accurate but also varied and meaningful for the user.

---

## Features

1. **Rating Prediction (Matrix Factorization)**

   * Predicts ratings for unseen movies using a latent factor model.
   * Evaluation metrics: **RMSE** and **MAE**.

2. **Top-K Recommendation**

   * Generates Top-10 movie recommendations for each user.
   * Evaluation metrics: **Precision@10**, **Recall@10**, **NDCG@10**, **MAP@10**.

3. **Diversity and Novelty**

   * Ensures recommendations are genre-diverse.
   * Metrics: **Intra-list Diversity**, **Novelty**, **Genre Coverage**.

4. **Explainable Recommendations**

   * Provides reasons for each recommended movie based on user interests and popular choices among similar users.

---

## Dataset

* **Ratings Data**: User-movie ratings.
* **Movies Data**: Movie metadata (title, genres).
* **Links Data**: External IDs (IMDB, TMDB).
* **Tags Data**: User-assigned movie tags.

**Data Preprocessing:**

* Removed all missing values to ensure consistent and reliable evaluation.
* One-hot encoded movie genres for content-based filtering.

---

## Methodology

1. **Data Preparation**

   * Split user ratings into **train** (80%) and **test** (20%) sets.
   * Created user–movie matrices for collaborative filtering.

2. **Content-Based Filtering**

   * Constructed a user profile based on genres of liked movies (ratings ≥ 4).
   * Calculated similarity scores of unseen movies to the user profile.

3. **Collaborative Filtering**

   * Used **cosine similarity** on user–movie rating matrix to find similar movies.
   * Predicted scores for unseen movies based on similarity to liked movies.

4. **Hybrid Recommendations**

   * Combined content and collaborative scores using a weighted factor **α = 0.7**.
   * Normalized scores to handle different scales.

5. **Diversity-Aware Re-ranking**

   * Applied a re-ranking algorithm to limit the number of movies per top genre.
   * Added popularity-based adjustments for novelty and diversity.

6. **Evaluation Metrics**

   * **Rating Prediction**: RMSE, MAE.
   * **Top-K Ranking**: Precision@10, Recall@10, NDCG@10, MAP@10.
   * **Diversity & Novelty**: Genre coverage, intra-list diversity, popularity-normalized hits.

---

## Results

**Evaluation over 5 users:**

* **Average Precision@10**: 10.00%
* **Average Recall@10**: 9.32%
* **Average Genre Coverage@10**: 15.20 genres
* **RMSE**: 5.5820
* **MAE**: 1.9813
* **NDCG@10**: 0.0
* **MAP@10**: 0.0
* **Intra-list Diversity**: 0.749
* **Novelty**: 12.696

> These metrics indicate a balanced hybrid system with good diversity and novelty, though there is room to improve ranking-based accuracy.

---

## Usage

```python
# Import libraries
import pandas as pd

# Load datasets
rating_data = pd.read_csv('ratings.csv')
movies_data = pd.read_csv('movies.csv')

# Generate hybrid recommendations for a user
recommendations = hybrid_recommend(user_id=604)
top_diverse = diversify_recommendations(recommendations, user_top_genres=['Action','Drama','Thriller'], K=10)

print(top_diverse)
```

---

## Limitations

1. **Data Sparsity**: Limited ratings per user may affect collaborative filtering accuracy.
2. **Cold Start Problem**: New users or new movies have little to no historical data.
3. **Alpha Sensitivity**: Changing the weight between content and collaborative filtering affects results.

---

## Acknowledgments

This project was completed as part of a **ReelSense recommendation system challenge**. Your feedback and suggestions are greatly appreciated to improve this work.

---
