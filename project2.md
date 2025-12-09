# Project 2: Predicting High Doctor Visits

## Introduce the Problem
This project looks at whether a patient will have a **high number of doctor visits** (here, 4 or more per year) based on their health and basic demographic information. In other words, it is a classification problem: the goal is to separate people into "high" and "low" doctor-visit groups so we can get a better sense of who might need more care.

## Introduce the Data
The dataset used is the **NPHA Doctor Visits** dataset. It includes information about patients' physical health, mental health, dental health, and some basic socioeconomic factors.
*   **Source:** NPHA Doctor Visits Dataset
*   **Key Features:**
    *   `Phy_Health`: Physical health rating.
    *   `Men_Health`: Mental health rating.
    *   `Age`: Age category.
    *   `Stress`: Stress levels.

## Pre-processing the Data
1.  **Renaming Columns:** Spaces were removed from column names so they are easier to work with in code.
2.  **Target Variable Creation:** The original `Number_of_Doctors_Visits` column was a number that could take many values. It was turned into a yes/no style target so we could focus on "High Usage":
    *   **0 (Low Visits):** Less than 4 visits.
    *   **1 (High Visits):** 4 or more visits.
3.  **Scaling:** `StandardScaler` was used to put all numeric features on a similar scale. This helps models like KNN and Logistic Regression, which are sensitive to differences in feature size (for example, Age versus Stress Level).
4.  **Trouble Sleeping Feature:** The dataset documentation says the "Trouble Sleeping" feature should be coded as 0 = No and 1 = Yes, but in the actual data this column sometimes takes values higher than 1 (for example, 2 or 3), which looks more like different levels of trouble sleeping. To keep things simple and closer to the documentation, a new yes/no column `Trouble_Sleeping_Binary` was created: 0 means no trouble sleeping, and any value above 0 is treated as "has trouble sleeping." This makes the model easier to work with, but it does lose some detail about how severe the sleep problems are.

## Data Understanding & Modeling
Three different models were tried for this classification problem:

1.  **Logistic Regression:** A linear model that provides interpretable coefficients.
2.  **K-Nearest Neighbors (KNN):** A distance-based classifier.
3.  **Decision Tree:** A tree-based model that captures non-linear relationships.

### Model Performance
*   **Logistic Regression Accuracy:** 0.706
*   **KNN Accuracy:** 0.657
*   **Decision Tree Accuracy:** 0.720

![Confusion Matrices](Project2\Images\confusion_matrices.png)

## Storytelling & Insights
Looking at the feature importance plots, **Physical Health (`Physical_Health`)** clearly stands out as the strongest signal across both models. **Mental Health (`Mental_Health`)** also shows up as important, especially in the decision tree, which tends to split on those two first.

The models also pick up on a few other patterns:
*   People with more problems related to sleep (for example, bathroom needs or pain keeping them up) tend to be more likely to land in the high-visits group.
*   Employment status and race show up with non‑zero importance too, which hints that work and background may also play some role in how often someone goes to the doctor.

![Feature Importance – Logistic Regression](Project2/Images/feature_importance_logreg.png)
![Feature Importance – Decision Tree](Project2/Images/feature_importance_tree.png)

Overall, this still points toward the idea that worse physical and mental health go hand in hand with more frequent doctor visits, and that sleep issues and some socioeconomic factors (like work status) are also part of the story.

## Impact Section
*   **Resource Allocation:** If a model like this works well, it could help clinics and hospitals plan staff and resources around people who are more likely to visit often.
*   **Potential Harm:** If used in the wrong way (for example, by an insurance company), this kind of model could be used to unfairly raise prices or limit options for people who already have health problems or high stress.
*   **Missing Perspectives:** The dataset does not include detailed medical history or any deeper background information. It is based on self-reported scores, which can be biased (for example, someone might under-report their stress or sleep problems), so the picture is not complete.

## References
1. NPHA Doctor Visits Dataset.
2. Scikit-learn documentation.

## Code
[Link to Project 2 Notebook](https://github.com/adampang27/adampang27.github.io/blob/main/Project%202/Project2.ipynb)