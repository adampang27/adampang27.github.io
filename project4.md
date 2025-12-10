# Project 4: Clustering Cat Breeds

## Introduce the Problem
Cats are one of the most popular pets in the world, but how different are they really? In this project, I am using **clustering techniques** to see if we can find natural groupings of cat breeds based on their physical traits, lifestyle, and caretaking patterns. 

Instead of just relying on breed labels, I want to see what the data says. The main questions I am trying to answer are:
*   Do cats naturally group together by breed, or do they form clusters based on other things like size or activity level?
*   Which features (like body length, outdoor access, or play time) are the most important for defining these groups?
*   Do different clustering algorithms (K-Means vs. Agglomerative) find the same patterns?

## What is Clustering and How Does It Work?
Clustering is a way of grouping data points so that items in the same group (or "cluster") are more similar to each other than to those in other groups. For this project, I used two different methods:

1.  **K-Means Clustering:** This algorithm tries to find $k$ center points (centroids) and assigns every cat to the nearest center. It keeps moving the centers until the groups are stable. It works best when clusters are round and roughly the same size.
2.  **Agglomerative Clustering:** This is approach starts up from the bottom. It starts by treating every single cat as its own cluster and then keeps merging the two most similar clusters until we reach the desired number of groups. It builds a hierarchy like a family tree.

To decide which method and how many clusters were best, I looked at metrics like the **Silhouette Score** (how distinct the clusters are) and the **Davies–Bouldin Index** (how well-separated they are).

## Introduce the Data
The dataset used for this analysis is `cat_breeds_clean.csv`. It contains information about various cat breeds, including their physical stats and daily lives.

*   **Source:** Provided course dataset (`cat_breeds_clean.csv`).
*   **Key Features:**
    *   **Physical:** `Body_length`, `Weight`, `Fur_colour_dominant`, `Eye_colour`.
    *   **Lifestyle:** `Allowed_outdoor`, `Owner_play_time_minutes`, `Sleep_time_hours`.
    *   **Demographics:** `Breed`, `Age_in_years`, `Gender`, `Country`.

## Data Understanding / Visualization
Before diving into the models, I explored the data to understand what I was working with.
*   **Data Integrity:** I checked for missing values and confirmed the data types were correct.
*   **Distributions:** I looked at histograms of numeric features. For example, `Owner_play_time_minutes` varied a lot, while `Sleep_time_hours` was mostly between 8 and 20 hours.
*   **Geography:** The data includes latitude and longitude, suggesting that where the cat lives might be a factor in the analysis.

## Pre-processing the Data
To get the data ready for clustering, I followed these steps:

1.  **Fixing Booleans:** Columns like `Neutered_or_spayed` and `Allowed_outdoor` were stored as text ("TRUE"/"FALSE"). I converted them to actual boolean values so the computer could understand them.
2.  **One-Hot Encoding:** Machine learning models can't read text like "Blue Eyes" or "Tabby Pattern." I used One-Hot Encoding to turn these categorical features into numbers (0s and 1s).
3.  **Scaling:** Clustering algorithms calculate "distance" between points. If one feature has huge numbers (like `Owner_play_time_minutes`) and another has small numbers (like `Age_in_years`), the big numbers will dominate the results. I used `StandardScaler` to put everything on the same scale.
4.  **Dropping Redundancies:** I removed `Age_in_months` because it is perfectly correlated with `Age_in_years`, and keeping both would just confuse the model.

## Modeling (Clustering)
I experimented with different numbers of clusters ($k$) ranging from 2 to 6.
*   I ran **K-Means** for each $k$ and calculated the Silhouette Score.
*   I picked the $k$ with the best score and then ran **Agglomerative Clustering** with that same number to compare the results.
*   I also calculated the **Adjusted Rand Index (ARI)** to see how well my clusters matched the actual Breed labels. This was just for curiosity—since clustering is unsupervised, we don't usually have "true" labels to check against!

### Model Performance
*   **Best k:** 2
*   **Silhouette Score:** 0.179
*   **Davies-Bouldin Index:** 2.146
*   **Adjusted Rand Index (K-Means):** 0.014
*   **Adjusted Rand Index (Agglomerative):** 0.027

The low ARI scores suggest that the natural clusters found by the algorithms do **not** align well with the breed labels. This means the cats are grouping based on other traits (like geography or size) rather than just their breed.

## Storytelling (Cluster Analysis)
After forming the clusters, I analyzed the "profiles" of each group to see what made them unique.
*   **Cluster Profiles:** I looked at the average weight, play time, and sleep time for each cluster.
*   **Visualizing Separation:** I used **PCA (Principal Component Analysis)** to combine the data down to 2 dimensions so I could plot it. This helped me see if the clusters were well-separated or if they overlapped a lot.

**Insights:**
The analysis revealed two main clusters that seem to be driven largely by **geography** and **size**:

*   **Cluster 0:**
    *   **Location:** Average Latitude ~48.85, Longitude ~-12.62 (Europe/France region).
    *   **Physique:** Smaller cats (Avg Body Length: 36.4 cm, Weight: 4.2 kg).
    *   **Age:** Younger on average (~2.8 years).
    *   **Lifestyle:** Slightly higher play time (26.7 mins).

*   **Cluster 1:**
    *   **Location:** Average Latitude ~41.90, Longitude ~-87.63 (USA/Chicago region).
    *   **Physique:** Larger cats (Avg Body Length: 48.4 cm, Weight: 6.2 kg).
    *   **Age:** Older on average (~6.0 years).
    *   **Lifestyle:** Slightly lower play time (21.0 mins).

It turns out the biggest difference wasn't "Indoor vs. Outdoor" or "Tabby vs. Solid," but rather **where the cats lived** and their **physical size**. The European cats in this dataset tended to be smaller and younger, while the American cats were larger and older. This explains why the clusters didn't match the breeds—the geographic signal was stronger than the breed signal!

![PCA Cluster Visualization](Project4/Images/pca_clusters.png)

## Impact Section
*   **Potential Benefits:** This kind of analysis could help animal shelters match cats to owners based on lifestyle (e.g., "needs high activity") rather than just breed stereotypes. It could also help pet product companies target specific segments of cat owners.
*   **Potential Harm:** If people take these clusters too seriously, they might stereotype cats even more. For example, assuming all cats in a certain cluster are "friendly" could lead to bad adoption matches if an individual cat is actually shy.
*   **Missing Perspectives:** The data is self-reported, so "Play Time" might be exaggerated by owners. We also lack medical history, which is a huge part of a cat's life.

## References
*   Scikit-learn Documentation: [Clustering](https://scikit-learn.org/stable/modules/clustering.html)
*   Seaborn Documentation: [Visualizations](https://seaborn.pydata.org/)
*   Joanna Nplkrk. "It's Raining Cats" dataset. Kaggle. https://www.kaggle.com/datasets/joannanplkrk/its-raining-cats

## Code
[Link to Project 4 Notebook](https://github.com/adampang27/adampang27.github.io/blob/main/Project4/Project4.ipynb)
