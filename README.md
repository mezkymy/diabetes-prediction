# Diabetes Prediction Model
Data Source: https://www.kaggle.com/datasets/iammustafatz/diabetes-prediction-dataset

[NBViewer Link](https://nbviewer.org/github/mezkymy/diabetes-prediction/blob/main/Diabetes_Prediction.ipynb)

Context (copied from Kaggle):

The Diabetes prediction dataset is a collection of medical and demographic data from patients, along with their diabetes status (positive or negative). The data includes features such as age, gender, body mass index (BMI), hypertension, heart disease, smoking history, HbA1c level, and blood glucose level. This dataset can be used to build machine learning models to predict diabetes in patients based on their medical history and demographic information. This can be useful for healthcare professionals in identifying patients who may be at risk of developing diabetes and in developing personalized treatment plans. Additionally, the dataset can be used by researchers to explore the relationships between various medical and demographic factors and the likelihood of developing diabetes.


# Data Exploration Insights
![Result of Pair Plot](https://github.com/mezkymy/diabetes-prediction/assets/79908491/40382d26-6d93-43fa-9b87-21872d80080c)

Based on the pair plot, we can gather some insights visually:
1. As stated in the data source, blood glucose level is one of the key indicator of diabetes. It is proven by visually looking at the distribution based on hue, where above 200 there are no patients that are not diagnosed with diabetes, while only a relatively small portion of patients with lower than 200 blood glucose level are diagnosed with diabetes
2. Furthermore, HbA1c_level or the measure of a person's average blood sugar level over the past 2-3 months segments patients even more, where those with blood glucose level somewhere between 100-150 but also with HbA1c level above ~7 are diagnosed with diabetes. This seperates the small portion of patients mentioned on point 1
3. No patients with blood glucose level above 200 have a HbA1c level of below ~5. At the same time, no patients with lower than ~125 blood glucose level have a HbA1c level of above ~7. Since blood glucose level are measured at a given time while HbA1c are measured on average over the past 2-3 months, this shows that both features are indeed correlated to each other, although blood glucose level at a given time might change drastically compared to its average over 2-3 months
4. Judging visually, a higher age means a higher risk of having diabetes, while hypertension and heart disease does not always indicate diabetes. Body mass index also are not visually correlated to diabetes
5. BMI are either heavily skewed, or there are some outliers that might need to be treated or removed

# Modeling
![gambar](https://github.com/mezkymy/diabetes-prediction/assets/79908491/0ad25d10-299f-4a3b-ba0a-2846c89cdc56)
In this project, five model types are used and compared with each other, which are:
1. Decision Tree
2. Random Forest
3. Logistic Regression
4. KNN
5. XGBoost

The third iteration of feature combinations which includes the features `age`, `bmi`, `HbA1c_level`, `blood_glucose_level`, `hypertension`, and `heart_disease` produces the best model with the lowest recall score achieved by Random Forest and XGBoost models. Tuning the Random Forest model, it achieved around 95% recall score on both train and test data. 

# Model Conclusions
Comparing all four iterations of modeling based on its recall score, we can see that the third iteration would be the ideal conditions to create the model, where the features used are all of the original features excluding gender, which have a very low correlation with all other features and also the target. On the result of the third iteration, we can also see that there are two models that have a relatively better score compared to others, which is **Random Forest** and **XGBoost**.

Although the model shaped by hyperparameter tuning the Random Forest model have a high enough recall and accuracy score while preventing overfitting compared to the base model, its precision score is noticably low. Depending on the use case, this might not be a huge concern since the amount of False Negatives (predicted 0 or non-diabetes, actual 1 or diabetes) are minimalized on the model. Note that a 95% recall score means that there is still a 5% rate of False Negatives occuring, which is still pretty significant considering that for medical purposes failing to detect a disease may lead to loss of lives, even at a 1% rate.

Since the split between the predicted class of 1 (predicted with diabetes) which are actually diagnosed with diabetes (1) or not (0 or False Positive) are almost 1:2, there will still be more patients that does not actually have diabetes compared to patients that actually have diabetes in the diabetes-predicted class. If this model is to be deployed, more thorough physical examinations should still be conducted on patients predicted with diabetes. 

This model can be used to quickly scan through patients but manual examinations are still necessary to prevent misdiagnosis and mistreatment. The model should not be used to determine diabetes on a patient without any additional checks, and more data and information should be collected to improve the performance of model even further.

