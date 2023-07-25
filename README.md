[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/JDiabl0/binder-framework/master)


Launch the Notebook here: https://mybinder.org/v2/gh/JDiabl0/binder-framework/master

# Predicting Cadets Likely to Struggle in Physics I
Jason M. Dahl, PhD

### Capstone Showcase Recording: https://youtu.be/e7Yg1mQUiQk

## Summary
This tool is a machine learning (ML) model that predicts the cadets most likely to struggle in Physics I based on their prior performance at the USCGA and in high school, for early intervention to provide academic support. 

## Problem Statement

The United States Coast Guard Academy (USCGA) recruits high-achieving students globally. However, every year, some cadets struggle to pass Physics I. Failure to pass
Physics I leads to several undesirable consequences, including a lower GPA, delayed graduation and deployment, and even disenrollment from the Academy. Early
intervention is essential, and academic support programs are available for struggling cadets. However, identifying at-risk cadets is challenging as they are often only
identified after failing exams. This tool aims to predict at-risk cadets at the start of the semester to get them into academic support programs as soon as possible.
Its purpose is to prevent an unfavorable outcome in Physics I, defined as a final grade of C- or worse.

Both training and prediction data require access to cadet personally identifiable information (PII), including grades and GPAs. Therefore, the tool is presented as a
Jupyter notebook, intended for use by the USCGA Vice Provost for Academic Affairs or their designee, (i.e the Physics I Course Coordinator).

## Project

The training data for the model consists of institutional data for cadets who took Physics I between 2017-2022, including high school GPA, standardized test scores,
initial math placement, college GPA, and prior grades in Calculus I and Physics I (if repeating). The outcome was determined from final Physics I grades and coded as 
1 if the cadet earned a grade of C- or worse (likely at-risk) or 0 if the cadet earned a score of C or better (likely successful). The data was cleaned, and
categorical data were One-Hot-Encoded for training. Only about 1 in 15 cadets in the training data was unsuccessful, so Synthetic Minority Oversampling
(BorderlineSMOTE) was used to balance the classes after splitting into training and test sets.

Classification was done using logistic regression, and the logistic regressor regularization parameter C was tuned using GridsearchCV. However, the best value for C
varied widely depending on which data was randomly selected into the training set. Therefore, the grid search was wrapped in a function that ran the grid search 1000
times, and the median value for C was used for the final fitting step.

Since the goal was to identify the most at-risk cadets, the precision of at-risk predictions was mapped, resulting in a threshold of 0.95 probability of a cadet 
being at risk being chosen for early referral for academic support. Locally Interpretable Model-Agnostic Explanations (LIME) were used to further visualize the 
likely reasons for these cadets' predictions, helping in choosing the best interventions for each cadet.





# Using Binder to Host your Notebooks
[Binder](https://mybinder.org) is a great and free service that makes it easy for someone to share their Jupyter notebooks for others to both view and run. Binder works by taking a GitHub repository and building a [Docker](https://www.docker.com) image. Using [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/), Binder runs a Docker container of the built Docker image.
