# DA5401 – Assignment 8

**Name:** Anan Madhav T V  
**Roll Number:** MM22B013

---

## 📂 Folder Structure

├── DA5401_A8_MM22B013.ipynb  
├── hour.csv  
└── README.md

---

## ⚙️ How to Run
1.  Open the notebook `DA5401_A8_MM22B013.ipynb` in **Jupyter Notebook** or **Google Colab**.
2.  Make sure the dataset file `hour.csv` is in the same directory.
3.  Ensure you have the required Python libraries installed (pandas, numpy, scikit-learn, matplotlib).
4.  Run all cells sequentially to reproduce the models, results, and plots.

---

## 📝 Assignment Work

This assignment focuses on **Ensemble Learning** to solve a complex, time-series-based **regression problem** using the **UCI Bike Sharing Demand Dataset**.

The goal was to apply and compare three primary ensemble techniques (Bagging, Boosting, and Stacking) to accurately forecast the total count of rented bikes (`cnt`) and evaluate their effectiveness in minimizing the **Root Mean Squared Error (RMSE)**.

1.  **Data Preparation:**
    * Loaded the `hour.csv` dataset.
    * Dropped irrelevant columns (`instant`, `dteday`, `casual`, `registered`).
    * Applied One-Hot Encoding to categorical features (`season`, `weathersit`, `mnth`, `hr`, `weekday`).
    * Split the data into training and testing sets.

2.  **Baseline Modeling (Part A):**
    * Trained a single **Decision Tree Regressor** (`max_depth=6`).
    * Trained a single **Linear Regression** model.
    * The `Linear Regression` (RMSE: 100.41) was identified as the better-performing baseline.

3.  **Ensemble Techniques (Part B & C):**
    * **Bagging:** Implemented a `BaggingRegressor` using Decision Trees as base estimators to analyze variance reduction.
    * **Boosting:** Implemented a `GradientBoostingRegressor` to analyze bias reduction.
    * **Stacking:** Implemented a `StackingRegressor` with a `Ridge` meta-learner to combine the predictions of diverse base learners (`KNeighborsRegressor`, `BaggingRegressor`, and `GradientBoostingRegressor`).

4.  **Interpretation (Part D):**
    * Calculated and compared the **RMSE** for all five models.
    * Created residual plots to visually demonstrate **bias vs. variance reduction**.
    * Analyzed why the ensemble methods, particularly Stacking, outperformed the single baseline models.

---

## ✅ Conclusion


**Best-Performing Model:** The **Stacking Regressor** was the best-performing model, achieving the lowest RMSE of **49.53**. It was followed very closely by the **Gradient Boosting Regressor** with an RMSE of **49.99**.

**Why it Outperformed the Baseline:**
* **Bias-Variance Trade-off:** The baseline models (Linear Regression at 100.47 and Decision Tree at 118.46) suffered from high bias. They were far too simple to capture the complex, non-linear patterns in the bike rental data, resulting in high errors.
* **Ensemble Improvements:** The GradientBoostingRegressor (RMSE 49.99) achieved a massive performance increase, cutting the baseline error by more than 50%. This confirms the main problem was high bias, which Gradient Boosting is specifically designed to correct. The BaggingRegressor (RMSE 112.34) performed poorly, as its low-variance base model (max_depth=6) couldn't fix the underlying bias.
* **Stacking's Advantage (Model Diversity):** The StackingRegressor (RMSE 49.53) won by a very slim margin. It gained its slight edge by leveraging model diversity. It combined the highly accurate GradientBoostingRegressor with other diverse models (KNeighborsRegressor and BaggingRegressor). The Ridge meta-learner learned to blend these predictions, squeezing out a final, small improvement that was slightly more accurate and robust than the Gradient Boosting model alone.
