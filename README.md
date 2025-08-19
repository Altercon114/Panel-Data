### README: U.S. Airline Panel Data Analysis

This repository contains an econometric analysis project focused on **panel data** within the U.S. airline industry. The analysis uses a dataset spanning 90 observations across 6 airlines over 15 years (1970-1984). The primary goal is to identify the most suitable panel data model and analyze the factors that influence the airlines' total costs.

---

### Dataset Description

The dataset is a subset of a larger collection originally compiled by Christensen Associates. It includes the following variables:

* `Airline`: The identifier for each airline (entity).
* `Year`: The year of the observation (time).
* `Response`: The total cost of the airline, in thousands of dollars.
* `Revenue`: Output, in billions of revenue passenger miles.
* `Fuel_price`: The price of fuel.
* `Load_factor`: The load factor, representing the average fleet capacity utilization.

---

### Project Structure

The analysis is conducted in a Python environment using libraries such as `pandas`, `statsmodels`, and `linearmodels`. The notebook `Panel Data Airlines Project.ipynb` is structured into the following sections:

1.  **Functions**: This section defines custom functions for panel data analysis, including:
    * `check_panel_balanced`: A function to verify if the panel data is balanced. The result shows that the panel is **balanced**, as each airline has observations for all 15 years.
    * `hausman`: A function that performs a robust Hausman test to handle potential singularities, which is crucial for comparing fixed and random effects models.
    * `_lsdv_and_Ftests`: A helper function to execute LSDV (Least Squares Dummy Variable) F-tests, used to determine if fixed effects are necessary.
    * `diagnosticos_panel`: A function that runs key diagnostics such as VIF for multicollinearity, the Breusch–Pagan test for heteroscedasticity, and the Durbin–Watson statistic for autocorrelation.
    * `seleccionar_modelo_panel`: The main function that automates the model selection process by fitting various panel models and choosing the most appropriate one based on statistical tests.

2.  **Getting to Know the Dataset**: This section covers loading, inspecting, and preprocessing the data, including renaming columns and setting the MultiIndex for panel analysis.

3.  **Panel Data Analysis**: This section applies the `seleccionar_modelo_panel` function to conduct the full analysis and retrieve the results of the selected model.

---

### Analysis Conclusions

The analysis concludes that a **Fixed Effects model with both entity and time effects (`FE_ambos`)** is the most appropriate for this dataset.

* **Model Selection**: The **Hausman test** rejects the null hypothesis, indicating that the Fixed Effects model is superior to the Random Effects model due to a significant correlation between unobserved effects and the independent variables.
* **Model Performance**: The selected model has an R-squared value of **0.8137**, suggesting that over 81% of the variation in airline total cost is explained by the model's variables.
* **Variable Significance**: Of the three independent variables, only **Revenue** is a **statistically significant** predictor of cost (p-value of 0.0000). The coefficients for **Fuel_price** and **Load_factor** are not statistically significant.
* **Diagnostics**: The analysis detected **heteroscedasticity** and **possible positive autocorrelation**. However, the use of a `Clustered` covariance estimator in the final model helps to correct for these issues, ensuring more reliable standard errors. Multicollinearity is not a concern, as all VIF values are below 5.
