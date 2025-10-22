# Stroke Prediction (Supervised Classification)

## Overview
This project applies machine learning to predict the likelihood of a stroke based on individual health and demographic factors. The model provides insights that can help identify high-risk individuals potentially aiding early intervention and public health planning.

## Objectives
- Gain preliminary insights on the factors influencing stroke in individuals through EDA
- Preprocess and prepare the dataset for accurate model training.
- Develop and compare multiple machine learning models for prediction.
- Evaluate models using reliable performance metrics.
- Understand the main factors contributing to stroke occurrence.

## The Dataset
The dataset used is from [Kaggle’s Stroke Prediction Dataset](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset) and includes a mix of demographic, health, and lifestyle attributes.
<br>The target variable is `stroke` (1 = stroke occurred, 0 = no stroke)</br>
<br>**Feature Categories</br>**
- **Demographic Feature**
  - gender: Male, Female, Other
  - age
  - ever_married: No, Yes
  - work_type: Private, Govt_job, Self_employed, children, Never_worked
  - Residence_type: Urban or Rural

- **Health Features**
  - hypertension: (0 - no hypertension, 1 - otherwise)
  - heart_disease: (0 - no heart_disease, 1 - otherwise)
  - avg_glucose_level
  - bmi
 
- **Lifestyle features**
  - smoking_status: never smoked, formerly smoked, smokes, unknown
   
  ## Workflow
1. **Exploratory Data Analysis:**
    | Feature               | Finding                                                                                 |
    | --------------------- | --------------------------------------------------------------------------------------- |
    | **Age**               | Stroke patients were older on average (≈71 years) than non-stroke patients (≈43 years). |
    | **Avg Glucose Level** | Stroke patients had a higher average glucose (105.22 vs. 91.47).                          |
    | **BMI**               | The average patient is slightly overweight. Not much difference in stroke rate                                   |
    | **Gender**            | Males had a slightly higher stroke rate (5.1%) than females (4.7%).                     |
    | **Hypertension**      | Stroke rate is over **3x higher** among hypertensive patients (13.3%).                  |
    | **Heart Disease**     | Stroke rate is **4x higher** for those with heart disease (17.0%).                      |
    | **Ever Married**      | Married individuals show higher stroke rates (6.6%).                                    |
    | **Work Type**         | Stroke rate was highest among self-employed individuals (7.9%) and nearly non-existent among those who never worked or were children.                          |
    | **Residence Type**    | Urban residents have slightly higher stroke rates (5.2%).                               |
    | **Smoking Status**    | Former smokers are most prone (7.9%), possibly due to long-term health impact.          |


2. **Preprocessing**
    - Handled missing values with KNNImputer
    - Scaled numeric features
    - Encoded categorical features
    - Addressed target class imbalance with over-sampling technique (SMOTE)

3. **Modelling & Evaluation:** Implemented and compared the following models based on F1 Score
    - K-Nearest Neighbors
    - Logistics Regression
    - Decision Trees
    - Random Forest
    - Gradient Boosting Classifier
  **Best Model:** Logistic Regression: Good generalisation without overfitting. Precision - 16.9% | Highest Recall - 72.5% | Best F1 Score - 27.5% 

4. **Threshold Tuning:** Due to the class imbalance, the standard probability threshold of 0.5 was adjusted to t = 0.30 to improve detection of stroke cases.
    | Metric    | After Threshold = 0.30 |
    | --------- | ---------------------- |
    | Precision | **⬇️ 13.3%**              |
    | Recall    | **⬆️ 88.7%**              |
    | F1 Score  | **⬇️ 23.2%**              |

5. **Model Interpretation**
    Since Logistic Regression does not provide feature importance like tree-based models, interpretability was achieved using Feature Coefficient Analysis which helps to understand the direction and magnitude of each feature.
     <br>The model highlights `age `, `glucose level`, `hypertension`, `heart disease`, and `smoking` as key risk factors. In contrast,  active employment and non-smoking status act as protective factors.

6. **Future Work**
   - Implement SHAP for in-depth feature explanations
   - Train deep learning models for further improvements
   - Deploy Streamlit for interactive stroke risk prediction.
