🏡 Real Estate Price Prediction: Polynomial Regression

This project is an advanced extension of a previous [Linear Regression analysis]. The goal is to predict real estate prices per unit area based on various features such as location, age of the house, and proximity to amenities. 

While the Simple Linear Regression model provided a baseline, this project explores **Polynomial Regression** to capture non-linear relationships and interaction terms between features, resulting in significantly lower error rates.

## 📌 Project Overview
Real-world data is rarely purely linear. Features often interact with each other (e.g., the value of a location might depend on both latitude *and* longitude). 

**Why Polynomial Regression?**
1.  **Non-linear Relationships:** Standard linear models assume a straight-line relationship. Polynomial regression allows for curves (Log, Square, Cubic relationships).
    
2.  **Interaction Terms:** It considers scenarios where features are only significant when combined (e.g., Feature A × Feature B).

## 📂 Dataset Description
The dataset consists of **414 records** with **8 columns**.

| Feature | Description |
| :--- | :--- |
| **X1 Transaction Date** | The date of the transaction |
| **X2 House Age** | Age of the house in years |
| **X3 MRT Distance** | Distance to the nearest MRT station (meters) |
| **X4 Convenience Stores** | Number of convenience stores nearby |
| **X5 Latitude** | Geographic coordinate |
| **X6 Longitude** | Geographic coordinate |
| **Y House Price** | **(Target)** House price of unit area (10000 New Taiwan Dollar/Ping) |

## 📊 Exploratory Data Analysis (EDA)
Before modeling, I analyzed the correlations to understand feature importance.

* **Correlation Heatmap:** showed strong negative correlations between *House Price* and *Distance to MRT*, and positive correlations with *Number of Convenience Stores*.
* **Pairplot:** Revealed that many relationships were not perfectly linear, justifying the use of Polynomial features.

*(Please insert your Heatmap image here)*

## ⚙️ Methodology

### 1. Feature Engineering
Using Scikit-Learn's `PolynomialFeatures`, I transformed the original features to include:
* Higher-order terms ($X^2, X^3...$)
* Interaction terms ($X_1 \times X_2$, etc.)

### 2. Model Training & Evaluation
I split the data into Training (70%) and Testing (30%) sets and trained a Linear Regression model on the transformed polynomial features (Degree=2).

**Performance Metrics (Degree = 2):**
* **MAE (Mean Absolute Error):** 4.49
* **RMSE (Root Mean Squared Error):** 5.69
* **R² Score:** High accuracy on test data.

### 3. Comparison: Linear vs. Polynomial
Comparing the results with the previous Simple Linear Regression model shows a clear improvement:

| Metric | Simple Linear Regression | Polynomial Regression (Deg 2) | Improvement |
| :--- | :--- | :--- | :--- |
| **MAE** | 5.37 | **4.49** | ✅ Reduced Error |
| **MSE** | 45.88 | **32.40** | ✅ Significant Drop |
| **RMSE** | 6.77 | **5.69** | ✅ Better Fit |

> **Insight:** The Polynomial model reduced the Root Mean Squared Error (RMSE) by approximately **1.08 units**, indicating a much better fit for the complex real estate data.

## 📉 Bias-Variance Tradeoff (Selecting the Best Degree)
One major challenge with Polynomial Regression is **Overfitting**. As we increase the degree of the polynomial, the model tries to fit every single noise point in the training data.

I analyzed degrees ranging from **1 to 10** to find the "sweet spot".

* **Degree 1-2:** Error decreases for both Train and Test sets.
* **Degree 3+:** Training error continues to drop, but **Test error explodes**.

*(Please insert your "Polynomial Degree vs RMSE" plot here)*

### Analysis of the Plot:
* The **Train RMSE** (Blue line) keeps decreasing as complexity increases.
* The **Test RMSE** (Orange line) spikes drastically after Degree 2.
* **Conclusion:** **Degree 2** is the optimal complexity for this dataset. Anything higher results in severe overfitting.

## 🛠 Technologies Used
* **Python**
* **Pandas & NumPy** (Data Manipulation)
* **Matplotlib & Seaborn** (Visualization)
* **Scikit-Learn** (Preprocessing, Modeling, Metrics)

## 🚀 How to Run
1.  Clone the repository.
2.  Install dependencies: `pip install pandas numpy matplotlib seaborn scikit-learn`
3.  Run the Jupyter Notebook: `polynomial_regression.ipynb`

---
*Author:  Sheikh Mohammad Abdullah
