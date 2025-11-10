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

-   The **Stacking Regressor** achieved the **best performance** with the lowest **RMSE of 64.04**.
-   The baseline models (Linear Regression: 100.41, Decision Tree: 118.56) suffered from **high bias**, as they were too simple to capture the complex, non-linear patterns in the rental data.
-   **Gradient Boosting** (RMSE 79.90) and **Bagging** (RMSE 112.10) both offered significant improvements, with boosting being more effective at fixing the high-bias problem.
-   The **Stacking Regressor** won by leveraging **model diversity**. By training a meta-learner on the predictions of different types of models, it was able to learn their individual strengths and weaknesses, creating a hybrid model that was more accurate and robust than any single component.

**Final Recommendation:** The **Stacking Regressor** is the most suitable model for this forecasting task, as it provides the lowest prediction error by effectively managing the bias-variance trade-off through model diversity.
