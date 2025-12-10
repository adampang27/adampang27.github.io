# Project 4: Clustering Cat Breeds

## Introduce the Problem
Cats are one of the most popular pets in the world, but how different are they really? In this project, I am using clustering techniques to see if we can find natural groupings of cat breeds based on their physical traits, lifestyle, and caretaking patterns. 

Instead of just relying on breed labels, I want to see what the data says. The main questions I am trying to answer are:
*   Do cats naturally group together by breed, or do they form clusters based on other things like size or activity level?
*   Which features (like body length, outdoor access, or play time) are the most important for defining these groups?
*   Do different clustering algorithms (K-Means vs. Agglomerative) find the same patterns?

## What is Clustering and How Does It Work?
Clustering is a way of grouping data points so that items in the same group (or "cluster") are more similar to each other than to those in other groups. For this project, I used two different methods:

1.  K-Means Clustering: This algorithm tries to find k center points (centroids) and assigns every cat to the nearest center. It keeps moving the centers until the groups are stable. It works best when clusters are round and roughly the same size.
2.  Agglomerative Clustering: This is approach starts up from the bottom. It starts by treating every single cat as its own cluster and then keeps merging the two most similar clusters until we reach the desired number of groups. It builds a hierarchy like a family tree.

To decide which method and how many clusters were best, I looked at metrics like the Silhouette Score (how distinct the clusters are) and the Davies–Bouldin Index (how well-separated they are).

## Introduce the Data
The dataset used for this analysis is `cat_breeds_clean.csv`. It contains information about various cat breeds, including their physical stats and daily lives.

*   **Source:** Provided course dataset (`cat_breeds_clean.csv`).
*   **Key Features:**
    *   **Physical:** `Body_length`, `Weight`, `Fur_colour_dominant`, `Eye_colour`.
    *   **Lifestyle:** `Allowed_outdoor`, `Owner_play_time_minutes`, `Sleep_time_hours`.
    *   **Demographics:** `Breed`, `Age_in_years`, `Gender`, `Country`.

## Data Understanding / Visualization
*   Checked for missing values and basic data types.
*   Plotted histograms for key numeric features like `Owner_play_time_minutes` and `Sleep_time_hours`.
*   Looked at latitude and longitude to see whether location might matter.

## Pre-processing the Data
To prepare the data for clustering, I:

1.  Converted `Neutered_or_spayed` and `Allowed_outdoor` from text ("TRUE"/"FALSE") to boolean values.
2.  One-hot encoded the categorical columns so the models could work with them.
3.  Standardized the numeric features (for example, `Owner_play_time_minutes` and `Age_in_years`) with `StandardScaler`.
4.  Dropped `Age_in_months` because it carries the same information as `Age_in_years`.

## Modeling (Clustering)
I tried 2–6 clusters and, for each value of k, ran **K-Means** and then **Agglomerative Clustering**, comparing them with the Silhouette Score, Davies–Bouldin Index, and the Adjusted Rand Index (ARI) against the breed labels (as an external check).

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

    Overall, the clusters differed more by **location** and **size** than by things like coat pattern or indoor/outdoor status. Cats from the European locations in this dataset were generally smaller and younger, while the U.S. cats were larger and older, which helps explain why the clusters did not line up neatly with the breed labels.

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
