---
layout: default
title: "Project 1"

# Student Dropout Analysis
---

# Introduction

So as we all know higher education is a powerful gateway that unlocks opportunities for all people. However, not everyone is able to finish their educational goals and some outright fail out. 
In this analysis, we will be looking at the factors that could contribute to student dropout and what makes certain students succeed.

## Research Questions

1. **Prior Academic Performance:**  
   What is the relationship between a student's previous qualification grade or admission grade and their likelihood of dropping out or graduating?

2. **First-Semester Engagement:**  
   How does a student's engagement in the first semester (number of curricular units enrolled, approved, and grades) predict their final outcome?

3. **Socioeconomic Factors:**  
   How do scholarship status, tuition fee status, and parental education/occupation influence student dropout rates and academic success?

---

## The Dataset

The data comes from **UCI’s Machine Learning Repository**:  
[Predict Students' Dropout and Academic Success](https://archive.ics.uci.edu/ml/datasets/Predict+Students'+Dropout+and+Academic+Success).  

- **Size:** 4,424 student records  
- **Features:** 36 attributes related to enrollment, demographics, socioeconomic factors, and performance  
- **Key Features:** GDPR, tuition status, scholarship holder, previous qualification grade, age at enrollment  
- **Target Variable:** Categorizes students into **Dropout**, **Enrolled**, or **Graduate**

---

## Data Preprocessing
![Alt text](adampang27.github.io\images\Project1(Preprocessing1).png)
- No missing or null values were found.  
- Most features were numeric, with the exception of the target variable (categorical).

---

## Visualizations
![](Project1\Images\admission_grade_distribution.png)
![](Project1\Images\first_sem_units_approved.png)
![](Project1\Images\scholarship_status.png)

---

## Storytelling

Contrary to the common belief that high school performance is the best predictor of college success, our analysis reveals a more complex picture.  

The box plot shows that while graduates have a slightly higher median admission grade, the distributions for Dropouts and Graduates overlap significantly.  
For example, a student with a grade of **120** could end up in either category.

This highlights that many factors beyond academics (e.g., financial challenges, motivation, and personal connections) can influence student outcomes.

---

## Impact

This changes how we should think about helping students. 
To truly ensure that students are gaining the education they deserve, we need to find things out like: Are they engaged in class? Do they have substantial debt? 
The goal is to catch students who are struggling for any reason, not just an academic one.

