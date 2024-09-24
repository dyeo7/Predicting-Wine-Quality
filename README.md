## Google Advanced Data Analytics Capstone Project


# Predicting Wine Quality with Clustering and Classification Models

# Project Overview

The goal of this project is to model red wine quality based on a series of physicochemical tests, including measurements such as fixed acidity, volatile acidity, citric acid, residual sugar, chlorides, free and total sulfer dioxide, density, pH, sulphates, and alcohol content. Using these features, I aim to predict the wine's quality, scored on a scale of 0 to 10. Various machine learning techniques, including KMeans clustering, Logistic Regression, Random Forest, and XGBoost were used to explore patterns in the data and classify the wine's quality. The final XGBoost model achieved a robust AUC score of 0.94 and an accuracy of 92%, making it the best-performing model in the project.

# Business Understanding 

The goal is to model wine quality based on physicochemical tests (see [Cortez et al., 2009], http://www3.dsi.uminho.pt/pcortez/wine/).
The dataset is related to red variants of the Portuguese "Vinho Verde" wine. Due to privacy and logistic issues, only physicochemical (inputs) and sensory (the output) variables are available (e.g. there is no data about grape types, wine brand, wine selling price, etc.).

These datasets can be viewed as classification or regression tasks. The classes are ordered and not balanced (e.g. there are many more normal wines than excellent or poor ones).

# Data Understanding 

The dataset consists of 1,599 samples of red wine, with the following physicochemical properties: fixed acidity, volatile acidity, citric acid, residual sugar, chlorides, free sulfur dioxide, total sulfur dioxide, density, pH, sulphates, and alcohol content. The quality score, ranging from 0 to 10, was converted into a binary classification problem where scores of 7 or higher were considered high quality. The dataset was inherently imbalanced from the start, and now with my binary classification, a majority of the wines 1,382 classified as low quality and only 217 as high quality poses an imbalance for models.

![image](https://github.com/user-attachments/assets/d56e644f-afe8-4dbe-b72e-514fc5ccbfb2)

![image](https://github.com/user-attachments/assets/3683d248-b79d-4cd1-8488-7d4f5da2b9e5)

# Modeling and Evaluation 

### Clustering: KMeans clustering was performed to explore the relationship between alcohol content and wine quality. My first assumption was that the higher the alcohol%, the better the wine quality. 

Two main clusters emerged:
Cluster 0: Mostly low-quality wines (rating 5) with moderate alcohol content (9.2% to 12.6%).
Cluster 1: A small group of high-alcohol wines (up to 14.9%), but these still received low-quality ratings.
The inertia score for 5 clusters was 9,816, and the silhouette score for 2 clusters was 0.21, indicating that while clustering provided insights, alcohol content was not a significant predictor of quality.
![image](https://github.com/user-attachments/assets/bfd95aaf-0af0-48a7-886e-572ec8b287ca)
![image](https://github.com/user-attachments/assets/4dad0a2d-8376-4a54-9c24-2c74de8db529)


### Logistic Regression:

A Logistic Regression model was built, achieving an accuracy of 89%. However, it struggled with recall for high-quality wines, only achieving a recall score of 35%, showing that Random Forest outperformed Logistic Regression.

Performance Metrics:
Precision: 0.60
Recall: 0.35
F1 Score: 0.44
Accuracy: 89%


![image](https://github.com/user-attachments/assets/4ee3bfd3-a7f2-4660-9a03-31c17b7f14a3)
The confusion matrix revealed that while the model correctly identified 406 low-quality wines (TN) and 23 high-quality wines (TP), it also misclassified 42 high-quality wines as low-quality (FN) and 9 low-quality wines as high-quality (FP). This resulted in a recall of only 35% for high-quality wines, meaning the model struggled to detect a substantial portion of high-quality samples. Overall, Logistic Regression achieved a high accuracy but underperformed in recall for high-quality wine predictions.


### Random Forest: 
The Random Forest model was fine-tuned using GridSearchCV to address the inherent class imbalance and optimize hyperparameters such as max_depth, max_features, and n_estimators. The best model configuration significantly improved performance:

Before Tuning: The model struggled with the imbalanced classes, favoring the majority low-quality wines.
After Tuning: The optimized model achieved an AUC score of 0.89 and an accuracy of 90.2%, demonstrating improved generalization and sensitivity to high-quality wines. 

Precision: 0.70

Recall: 0.49

F1 Score: 0.57

Accuracy: 90.17%

AUC: 0.89

This model compared to the Logisitc Regression model provided the better balance between precision and recall, indicating a stronger performance in predicting wine quality.

![image](https://github.com/user-attachments/assets/352824f4-2c87-4af1-ad39-55dadb2ca703)

The confusion matrix revealed that the Random Forest model accurately identified 409 low-quality samples (TN) and 38 high-quality samples (TP), but it struggled with 27 high-quality samples misclassified as low-quality (FN) and 6 low-quality samples misclassified as high-quality (FP). This resulted in a precision of 0.70 and a recall of 48.7% for high-quality samples. The model achieved an F1 score of 0.57, indicating a balanced performance between precision and recall. With an overall accuracy of 90.2% and AUC score of 0.89, demonstrates that the model effectively differentiates between classes, though there is room to improve for high-quality predictions.


### XGBoost

The XGBoost model, while performing slightly worse than Random Forest in identifying high-quality wines (with fewer true positives), still demonstrated stronger overall performance across metrics such as accuracy and AUC score.

Performance Metrics:
Accuracy: 92%
Precision (class 0): 0.93
Recall (class 0): 0.99
F1-Score (class 0): 0.96
Precision (class 1): 0.85
Recall (class 1): 0.51
F1-Score (class 1): 0.63
ROC AUC Score: 0.941

Confusion Matrix:
True Positives (TP): 33 (correctly classified high-quality wines)
False Negatives (FN): 32 (high-quality wines incorrectly classified as low-quality)
True Negatives (TN): 409 (correctly classified low-quality wines)
False Positives (FP): 6 (low-quality wines incorrectly classified as high-quality)
Although XGBoost had fewer true positives for high-quality wines (33 TP compared to Random Forest’s 38), it achieved higher accuracy (92%) and a better ROC AUC score (0.941), making it the best overall model in terms of general performance.

Feature Importance in XGBoost Model

![image](https://github.com/user-attachments/assets/76dd0980-5dbd-4ddb-8c3a-bd17f5e89234)

These feature importance values provide insights into which physicochemical properties most strongly affect the quality of wine in the dataset.


