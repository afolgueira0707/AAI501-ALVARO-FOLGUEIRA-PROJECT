This project is a part of the AAI-500 course in the Applied Artificial Intelligence Program at the University of San Diego (USD).

Installation

To run, edit, or reproduce this project locally, follow these setup instructions:

    Clone the Repository:
    git clone https://github.com/your-username/stroke-prediction-ml.git
    cd stroke-prediction-ml

    Set Up a Virtual Environment (Recommended):
    python -m venv venv
    source venv/bin/activate

    Install Required Packages:
    pip install -r requirements.txt

    Run the Master Pipeline:
    Launch Jupyter Notebook or JupyterLab and run the central pipeline orchestrator:
    jupyter notebook pipeline.ipynb

Project Intro/Objective

Stroke remains a leading cause of global mortality and long-term disability, making early risk identification vital to prevent irreversible neurological damage. The primary goal of this project is to build an automated, high-sensitivity machine learning decision-support pipeline that evaluates demographic, lifestyle, and clinical factors to flag at-risk patients early.

Designed specifically for integration as a decision-support alert within clinical Electronic Health Record (EHR) systems, the model prioritizes Recall and ROC-AUC. By minimizing critical False Negatives, this system aims to ensure high-risk individuals receive timely, life-saving neurological evaluations before an acute event occurs.

Contributor

    Alvaro Folgueira

    Program: M.S. in Applied Artificial Intelligence, University of San Diego

Methods Used

    Machine Learning (Classification)

    Exploratory Data Analysis (EDA)

    Data Pre-Processing & Feature Engineering

    Synthetic Minority Over-sampling Technique (SMOTE)

    Hyperparameter Tuning (Grid Search & Cross-Validation)

    Decision Boundary / Threshold Optimization

    Data Visualization

Technologies

    Python 3.x

    Pandas, NumPy

    Scikit-Learn

    XGBoost

    Imbalanced-Learn (SMOTE)

    Matplotlib, Seaborn

    Jupyter Notebooks

Project Description
Overview & Data Source

This project utilizes a clinical dataset sourced from Kaggle containing 5,110 individual patient records across 10 predictor attributes and 1 binary target (stroke). The dataset was partitioned into a strict 70-15-15 split (Training, Validation, and Holdout Test) to ensure unbiased model evaluation.

Data Dictionary

    id (Identifier): Unique patient identifier

    gender (Categorical): Male, Female, or Other

    age (Continuous): Age of the patient (years)

    hypertension (Binary): 0 = No hypertension, 1 = Has hypertension

    heart_disease (Binary): 0 = No heart disease, 1 = Has heart disease

    ever_married (Binary): Yes or No

    work_type (Categorical): Private, Self-employed, Govt_job, children, Never_worked

    Residence_type (Binary): Urban or Rural

    avg_glucose_level (Continuous): Average blood glucose level (mg/dL)

    bmi (Continuous): Body Mass Index

    smoking_status (Categorical): formerly smoked, never smoked, smokes, Unknown

    stroke (Binary - Target): 1 = Patient had a stroke, 0 = No stroke

Modeling & Pipeline Approach

    Data Pre-Processing: Handled missing continuous values (~2.9% in bmi) via median imputation, applied log(1+x) transformations and RobustScaler to address right-skewed distributions, encoded categorical features via OneHotEncoder, and addressed extreme target imbalance (only 4.86% stroke cases) using SMOTE exclusively on training data.

    Base Model Evaluation: Benchmarked six baseline classifiers—Logistic Regression, SVM, KNN, Decision Trees, Random Forests, and XGBoost.

    Two-Step Tuning Strategy: Applied 5-fold cross-validation on SMOTE-balanced training data to tune hyperparameters for ROC-AUC, followed by probability threshold sweeps on raw validation data to optimize decision boundaries for high sensitivity (Recall).

    Champion Model: Selected Logistic Regression for its superior ability to minimize false negatives. On the unseen holdout test set, the tuned model achieved an 81.6% Recall (identifying 31 of 38 actual stroke cases) and a 0.8336 ROC-AUC at a 0.48 decision threshold.

Key Challenges & Roadblocks

    Extreme Target Imbalance: Standard models yielded high accuracy (>93%) by simply predicting the majority class, masking near-zero sensitivity to stroke cases.

    Precision-Recall Trade-off: Prioritizing high Recall to minimize missed diagnoses intentionally increased False Positives, requiring careful framing for clinical feasibility.

Project Deliverables

    Report Document: Located in project_directory/report (.docx)

    Presentation Slides: Located in project_directory/presentation/slides

    Video Recording: Located in project_directory/presentation/video

Acknowledgments

    Faculty and advisors in the Applied Artificial Intelligence (MS-AAI) program at the University of San Diego.

    Special thanks to students Marcelo Salvador and Roopleen Kaur for their support and guidance in understanding the subject matter and domain context.