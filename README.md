# Experiment 4: Multiple Regression Analysis (Fish Dataset)

## Aim
To perform Multiple Linear Regression on a dataset imported from a CSV file to analyze how multiple features together predict a dependent variable.

## Dataset
The dataset used for this experiment is `fish.csv` which contains real-world physical measurements of various fish species:
* **Independent Variables ($X$):**
  * `L`: Mean length derived from `Length1`, `Length2`, and `Length3`
  * `Height`: Vertical height of the fish
  * `Width`: Diagonal width of the fish
* **Dependent Variable ($Y$):**
  * `Weight`: Weight of the fish (in grams)

## Algorithm / Steps Followed
1. Import the required Python libraries (`numpy`, `pandas`, `matplotlib`, `scikit-learn`).
2. Load the fish dataset into a Pandas DataFrame using `pd.read_csv()`.
3. Display the dataset and inspect its columns.
4. Define the dependent ($Y$) and independent ($X$) variables.
5. Train the Multiple Linear Regression model using `LinearRegression()`.
6. Display the model coefficients (`model.coef_`), intercept (`model.intercept_`), and regression equation.
7. Predict target variable (`Weight`) values using `model.predict()`.
8. Evaluate model accuracy using the $R^2$ score (`r2_score()`).
9. Plot actual vs. predicted values for visual comparison.

## Functions and Methods Used

| Category | Function / Method | Purpose / Description |
| :--- | :--- | :--- |
| **Data Creation / Handling** | `pd.read_csv()` | Load the CSV dataset into a Pandas DataFrame |
| | `np.array()` / `pd.DataFrame()` | Create and manage numerical arrays and tabular data for regression |
| **Model Building (Scikit-learn)** | `LinearRegression()` | Initialize the Multiple Linear Regression model |
| | `model.fit()` | Train the regression model using multiple independent variables ($X$) and target ($Y$) |
| | `model.predict()` | Predict dependent variable values ($Y$) using the trained model |
| | `r2_score()` | Evaluate the accuracy of the regression model using the $R^2$ score |
| **Model Attributes** | `model.intercept_` | Retrieve the intercept (constant term) of the regression equation |
| | `model.coef_` | Retrieve the coefficients (slopes) for each independent variable |
| **Visualization (Matplotlib)** | `plt.plot()` | Plot actual and predicted weight values for comparison |
| | `plt.title()`, `plt.xlabel()`, `plt.ylabel()`, `plt.legend()`, `plt.show()` | Configure titles, axis labels, legend, and display the plotted figure |

## Program 

     import numpy as np
     import pandas as pd
     import matplotlib.pyplot as plt
     
     from sklearn.linear_model import LinearRegression
     from sklearn.metrics import r2_score
     
     # Load fish dataset
     df = pd.read_csv("Fish_length.csv")
     
     # Display dataset
     print("Fish Dataset:")
     print(df.head())
     
     # Calculate mean length
     df['L'] = (df['Length1'] + df['Length2'] + df['Length3']) / 3
     
     # Select independent and dependent variables
     X = df[['L', 'Height', 'Width']]
     Y = df['Weight']
     
     # Create Multiple Linear Regression model
     model = LinearRegression()
     
     # Train the model
     model.fit(X, Y)
     
     # Display coefficients and intercept
     print("\nCoefficients:")
     print(model.coef_)
     
     print("\nIntercept:")
     print(model.intercept_)
     
     # Display regression equation
     print("\nRegression Equation:")
     print("Weight =",
           model.intercept_,
           "+", model.coef_[0], "* L",
           "+", model.coef_[1], "* Height",
           "+", model.coef_[2], "* Width")
     
     # Predict weight
     y_pred = model.predict(X)
     
     # Calculate R2 score
     print("\nR2 Score:")
     print(r2_score(Y, y_pred))
     
     # Display actual and predicted values
     print("\nActual vs Predicted Weight:")
     print(pd.DataFrame({
         'Actual Weight': Y,
         'Predicted Weight': y_pred
     }).head(10))
     
     # Plot actual vs predicted values
     plt.figure(figsize=(8, 5))
     plt.plot(Y.values, label='Actual Weight', marker='o')
     plt.plot(y_pred, label='Predicted Weight', marker='x')
     
     plt.title("Actual vs Predicted Fish Weight")
     plt.xlabel("Fish Index")
     plt.ylabel("Weight (grams)")
     plt.legend()
     plt.grid()
     plt.show()
     
 ## Output

     Fish Dataset:
      Species  Weight  Length1  Length2  Length3   Height   Width
    0   Roach   259.1     25.1     27.2     29.9   8.8210  4.6136
    1   Bream   423.2     29.0     30.9     33.5  13.4218  5.6620
    2   Roach   151.1     21.4     23.2     25.2   7.2479  3.9580
    3   Perch   523.2     31.5     34.2     37.6   9.9794  5.5136
    4   Perch   355.7     27.3     29.9     32.9   8.7762  4.7713
    
    Coefficients:
    [  38.44144067   25.80398645 -107.6604105 ]
    
    Intercept:
    -495.38038500886614
    
    Regression Equation:
    Weight = -495.38038500886614 + 38.441440670641356 * L + 25.803986449763947 * Height + -107.66041049560657 * Width
    
    R2 Score:
    0.9139876519274813
    
    Actual vs Predicted Weight:
       Actual Weight  Predicted Weight
    0          259.1        288.829984
    1          423.2        438.192502
    2          151.1        159.928610
    3          523.2        492.198418
    4          355.7        371.925046
    5           72.9         25.273562
    6           12.7       -111.178205
    7          177.3        233.019362
    8           15.2        -81.752720
    9          573.8        538.785631

  <img width="552" height="370" alt="image" src="https://github.com/user-attachments/assets/de7fb2c1-8a6c-44f5-885f-29554a9e3838" />

## Result
Thus, Multiple Linear Regression was successfully implemented using Python and Scikit-learn on the fish dataset. The relationship between mean length, height, width, and fish weight was analyzed. The regression coefficients, intercept, predicted values, and R² score were calculated, and actual versus predicted fish weights were plotted for comparison.
