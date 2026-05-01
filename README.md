# IBM Applied Data Science Capstone — Loan Repayment Prediction

> **IBM Applied Data Science Professional Certificate** · Capstone Project
> > Classification models to predict whether a borrower will repay a loan — built end-to-end from raw data through model evaluation.
> >
> > ---
> >
> > ## Overview
> >
> > This is the final capstone project for the [IBM Applied Data Science Professional Certificate](https://www.coursera.org/professional-certificates/ibm-data-science) on Coursera. The goal was to apply the full data science workflow — data wrangling, exploratory analysis, feature engineering, and machine learning — to a real-world lending dataset and determine which classification algorithm best predicts loan repayment outcomes.
> >
> > ---
> >
> > ## The Dataset
> >
> > The dataset comes from the IBM Skills Network and contains historical loan records with the following key features:
> >
> > | Feature | Description |
> > |---|---|
> > | `Principal` | Loan principal amount (USD) |
> > | `terms` | Repayment term in days (7, 15, or 30) |
> > | `age` | Borrower's age |
> > | `education` | Borrower's highest education level |
> > | `Gender` | Borrower's gender |
> > | `dayofweek` | Day of week the loan was issued |
> > | `weekend` | Binary flag — was the loan issued on a weekend? |
> > | `loan_status` | **Target variable** — `PAIDOFF` or `COLLECTION` (defaulted) |
> >
> > - **346 records** after cleaning
> > - - **Binary classification** task: predict `PAIDOFF` vs `COLLECTION`
> >   - - Moderate class imbalance (~86% paid off, ~14% defaulted)
> >    
> >     - ---
> >
> > ## What I Did
> >
> > ### 1. Data Wrangling & Feature Engineering
> > - Loaded and inspected the raw CSV; handled missing values and data types
> > - - Converted `due_date` and `effective_date` to datetime, extracted day-of-week
> >   - - Created a `weekend` binary feature (loans taken on weekends showed different repayment patterns)
> >     - - One-hot encoded `Gender` and `education` for model compatibility
> >       - - Normalized continuous features (`Principal`, `terms`, `age`) using `StandardScaler`
> >        
> >         - ### 2. Exploratory Data Analysis
> >         - - Visualized repayment rates by loan term, education level, gender, and day of week
> >           - - Key finding: borrowers who took loans on weekdays had notably higher repayment rates
> >             - - Shorter loan terms (7 days) had lower repayment rates than longer terms
> >               - - Education level showed a meaningful correlation with repayment outcome
> >                
> >                 - ### 3. Model Training & Evaluation
> >                
> >                 - Trained and evaluated four classification algorithms using an 80/20 train/test split with `random_state=4`:
> >                
> >                 - | Model | Jaccard Score | F1 Score | Log Loss |
> > |---|---|---|---|
> > | K-Nearest Neighbors (KNN) | 0.74 | 0.66 | N/A |
> > | Decision Tree | 0.76 | 0.73 | N/A |
> > | Support Vector Machine (SVM) | 0.80 | 0.76 | N/A |
> > | Logistic Regression | 0.74 | 0.66 | 0.57 |
> >
> > **Best performer: SVM** with an RBF kernel — highest Jaccard and F1 scores.
> >
> > Hyperparameter tuning was performed for KNN (optimal `k=7`) and Decision Tree (optimal `max_depth=4`).
> >
> > ---
> >
> > ## Tech Stack
> >
> > - **Python 3** · **Jupyter Notebook**
> > - - `pandas` · `numpy` — data manipulation
> >   - - `matplotlib` · `seaborn` — visualization
> >     - - `scikit-learn` — preprocessing, model training, evaluation
> >       -   - `KNeighborsClassifier`, `DecisionTreeClassifier`, `SVC`, `LogisticRegression`
> >           -   - `StandardScaler`, `train_test_split`, `jaccard_score`, `f1_score`
> >            
> >               - ---
> >
> > ## Key Takeaways
> >
> > 1. **Feature engineering matters more than model choice** — the `weekend` and `dayofweek` features were among the most predictive, yet they weren't in the raw data.
> > 2. 2. **SVMs excel on small, well-scaled tabular datasets** — with only 346 rows and normalized features, SVM outperformed tree-based and distance-based methods.
> >    3. 3. **Class imbalance needs attention** — the ~86/14 split inflated accuracy; Jaccard and F1 gave a more honest picture of model performance on the minority class.
> >       4. 4. **EDA informs everything downstream** — the bar plots and cross-tabulations guided which features to keep and how to engineer new ones.
> >         
> >          5. ---
> >         
> >          6. ## Repository Structure
> >         
> >          7. ```
> > ibm-python-final-project-loan-analysis/
> > ├── README.md                  # This file
> > ├── notebook/
> > │   └── ML0101EN-Proj-Loan-py-v1.ipynb   # Main project notebook
> > └── data/
> >     └── loan_train.csv         # Training dataset
> > ```
> >
> > ---
> >
> > ## Certificate
> >
> > This project was completed as part of the **IBM Applied Data Science Professional Certificate** (10-course series) on Coursera — covering Python, data analysis, visualization, machine learning, and AI applications.
> >
> > ---
> >
> > *Built by [@anihc1978](https://github.com/anihc1978) · May 2026*
