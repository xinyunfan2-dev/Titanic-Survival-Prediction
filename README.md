# Titanic Survival Prediction

A machine learning classification project to predict passenger survival on the Titanic dataset.

This project demonstrates an end-to-end machine learning workflow, including:

- Exploratory Data Analysis (EDA)
- Missing value analysis and handling
- Feature engineering
- Feature selection
- Model training
- Kaggle submission generation


## Project Overview

The objective of this project is to build a machine learning model that predicts whether a passenger survived the Titanic shipwreck.

The project follows a complete machine learning pipeline:

Data Loading
      ↓
Exploratory Data Analysis
      ↓
Data Cleaning
      ↓
Feature Engineering
      ↓
Feature Selection
      ↓
Model Training
      ↓
Prediction & Submission


## Dataset

Dataset:

**Kaggle Titanic Competition**

https://www.kaggle.com/competitions/titanic


The dataset contains:

| File | Description |
|---|---|
| train.csv | Training dataset containing passenger information and survival labels |
| test.csv | Test dataset without survival labels |
| gender_submission.csv | Example Kaggle submission format |


### Target Variable

The prediction target is:

Survived

where:

0 = Did not survive
1 = Survived


## Technologies Used

### Programming Language

- Python


### Data Processing

- Pandas
- NumPy


### Data Visualization

- Matplotlib
- Seaborn


### Machine Learning

- Scikit-learn


### Model

- Random Forest Classifier


# Workflow


## 1. Data Loading

The dataset is loaded using Pandas.

The training dataset contains:

- Passenger information
- Feature variables
- Survival labels


The testing dataset contains:

- Passenger information
- Features for prediction


## 2. Exploratory Data Analysis (EDA)

The following analysis was performed:

- Dataset structure inspection
- Feature type classification
- Statistical summary
- Missing value analysis
- Feature distribution analysis
- Correlation analysis


Features were categorized into:

### Numerical Features

- Age
- Fare
- SibSp
- Parch


### Categorical Features

- Pclass
- Sex
- Embarked


### Text / ID Features

- PassengerId
- Name
- Ticket
- Cabin


## 3. Missing Value Handling

Missing values were analyzed and processed based on feature characteristics.


| Feature | Missing Handling Strategy |
|---|---|
| Embarked | Fill with mode |
| Age | Group-based median imputation |
| Cabin | Extract Deck information |
| Fare | Fill with median value |


### Age Imputation

Instead of using a simple global median, age values were estimated based on:

- Passenger class
- Family size


This preserves more information from passenger groups.


## 4. Feature Engineering

Additional features were created to improve model performance.


## Family Size

Created from:

FamilySize = SibSp + Parch + 1

This represents the total number of family members travelling together.


## Deck Extraction

Cabin information was transformed into deck information:

Cabin → Deck

Example:

C85 → C


## Title Extraction

Passenger names were processed to extract social titles.

Examples:

Mr
Mrs
Miss
Master
Rare


Rare titles were grouped together to reduce sparsity.


## IsAlone

Created a binary feature:

1 = Passenger travelled alone
0 = Passenger travelled with family


## Fare Per Person

Created:

FarePerPerson = Fare / FamilySize


This feature was tested during feature selection.


# Exploratory Findings


## Survival Analysis

Important observations:

- Female passengers had a significantly higher survival rate.
- Survival probability decreased from first class to third class.
- Passenger class and fare showed relationships with survival.
- Deck information provided additional predictive information.


# Feature Selection


Different feature combinations were evaluated using:

- Random Forest Classifier
- Stratified 5-Fold Cross Validation
- Accuracy metric


## Feature Experiments

| Feature Set | Mean CV Accuracy |
|---|---:|
| Baseline | 0.8182 |
| + Title | 0.8260 |
| + Title + IsAlone | 0.8249 |
| + Title + IsAlone + FarePerPerson | 0.8227 |
| + Title + FarePerPerson | 0.8249 |


Based on cross-validation results:

- Title improved model performance.
- IsAlone and FarePerPerson provided limited additional improvement.


# Final Feature Set


The final model uses:


Pclass
Sex
Age
Fare
Embarked
Deck
FamilySize
Title


# Model Training


## Random Forest Classifier


The final model was trained using:

RandomForestClassifier


Main parameters:

n_estimators = 300
max_depth = 4
min_samples_leaf = 3
random_state = 42


## Evaluation Method

The model was evaluated using:

5-Fold Stratified Cross Validation


Evaluation Metric:

Accuracy


Accuracy measures:

Correct Predictions / Total Predictions


# Submission


The final prediction file follows Kaggle submission requirements.


Format:

PassengerId,Survived


Example:

PassengerId,Survived
892,0
893,1
894,0


# Notebook

The complete implementation can be found in:

03_Titanic_Notebook.ipynb


The notebook includes:

- Data exploration
- Visualization
- Data preprocessing
- Feature engineering
- Model evaluation
- Submission generation


# Results

The final model achieved approximately:

Cross Validation Accuracy: 82.6%


# Future Improvements

Possible improvements include:

- Hyperparameter tuning
- XGBoost / LightGBM comparison
- Ensemble learning
- Feature interaction engineering
- Automated machine learning pipeline
- Model explainability analysis


# Author

**Xinyun Fan**

Computer Science Student  
City University of Hong Kong


GitHub:

https://github.com/xinyunfan2-dev
