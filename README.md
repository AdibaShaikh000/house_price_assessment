# House Selling Price Prediction

## Outline
- Objective
- Data Exploration and Preprocesing
- Model Training
- Model Evaluation
- Model Prediction Explanation
- Future Improvements


## Objective
Given a dataset of house prices, build a regression model to predict house prices

## Data Exploration & Preprocesing
- The dataset comprises 1000 entries and 10 columns
- The "ID" column serves as an identifier and is not considered a feature
- It encompasses 8 distinct features, detailed as follows:
1. OverallQual	: Overall quality rating of the house, ranging from 0 to 10
2. GrLivArea : Above ground living area in square feet
3. YearBuilt : Construction year of the house
4. TotalBsmtSF	: Total Basement Area in square feet
5. FullBath : Number of full bathroom
6. HalfBath : Number of half bathroom
7. GarageCars : Number of cars the garage can accomodate
8. GarageArea : Total Garage Area in square feet
- The target variable is the "SalePrice", which refers to the selling price of the house

### Observations
- **Null value absence:** The dataset exhibits absence of null values, indicating that there are no missing entries. Hence, there is no requirement for imputation techniques to handle missing data
- **Numerical Data:**  All columns in the dataset are of integer data type, suggesting the absence of categorical variables. This eliminates the requirement for encoding pre-processing step used to transform categorical data into numerical format.

### Data Visualization
#### Distribution of Sale Price
![Sale Price Distribution](https://github.com/AdibaShaikh000/house_price_assessment/blob/main/resources/data_visualization/sale_price_distribution.PNG)
- The distribution exhibits 3 modes
- For a multi-modal distribution, traditional regression models might struggle to capture its complexity
- Exploring ensemble models or advanced regression techniques would be advisable in this scenario

#### Mean Sale Price by Overall Quality
![Mean Sale Price by Overall Quality](https://github.com/AdibaShaikh000/house_price_assessment/blob/main/resources/data_visualization/mean_sale_price_by_overall_quality.PNG)


#### Mean Sale Price by Year Built
![Mean Sale Price by Year Built](https://github.com/AdibaShaikh000/house_price_assessment/blob/main/resources/data_visualization/mean_sale_price_by_year_built.PNG)
  
#### Scatter Plot of Sale Price vs Features
![Sale Price vs Features](https://github.com/AdibaShaikh000/house_price_assessment/blob/main/resources/data_visualization/sale_price_vs_featuress.PNG)
- The data exhibits high variance and randomness

#### Visualizing Garage Area
![Garage Area](https://github.com/AdibaShaikh000/house_price_assessment/blob/main/resources/data_visualization/garage_area_box_plot.PNG)
- The garage area spans from 0 to 1000, lacking any contextual details.
- This column contains erroneous data

#### Visualizing Living Area and Basement Area
![Living Area](https://github.com/AdibaShaikh000/house_price_assessment/blob/main/resources/data_visualization/living_area_box_plot.PNG)
![Basement Area](https://github.com/AdibaShaikh000/house_price_assessment/blob/main/resources/data_visualization/basement_area_box_plot.PNG)

- Basement areas span from 0 to 3500, with irregular values such as 1, 2, 6, and 8, indicating potential data quality issues
- Similarly, living areas ranges from 500 to 3500
- Approximately 44% of the houses in the dataset have basement areas exceeding their living areas, a relatively uncommon occurrence.

#### Correlation 
![Correlation Matrix](https://github.com/AdibaShaikh000/house_price_assessment/blob/main/resources/data_visualization/correlation_heatmap.PNG)
- "TotalBsmtSF" and "GarageArea" have a greater correlation with "SalePrice", although the correlation coefficients are relatively low.
- The correlations are generally weak, suggesting that these features may not be strong predictors of the "SalePrice" individually.
- There are no meaningful pattern in the data

## Model Training

### Train Test Split
The dataset was split into two sets:
Training Set: Comprising 70% of the data, i.e. 700 data points
Test Set: Consisting of 30% of the data, i.e. 300 data points.
Before model training, the dataset underwent shuffling to ensure randomness and prevent any bias in the model training process

### Data Normalization
Applied StandardScaler for data normalization, ensuring all features contribute equally to model training. It transforms the data distribution to have a mean of 0 and a standard deviation of 1. 

### Trained Model
Sequential ensemble method for minimizing prediction errors iteratively.
1. Linear Regression: Base line model for regression task
2. Ridge: Linear regression with L2 regularization to prevent overfitting
3. Lasso: Linear regression with L1 regularization for feature selection
4. Random Forest Regressor: Ensemble model that combine results from multiple decision tree (Bagging)
5. Gradient Boosting Regressor: Sequential ensemble method for minimizing prediction errors iteratively (Boosting)

This comprehensive approach allows us to compare the predictive capabilities of each model and identify the one that best suits our data and objectives

### Cross validation
During training, KFold cross-validation with 5 folds was employed.

### Model Selection
|             Model            |  Accuracy  |
|------------------------------|------------|
| Linear Regression            |  -0.02118  |
| Ridge                        |  -0.02117  |
| Lasso                        |  -0.02118  |
| Random Forest Regressor      |  -0.09059  |
| Gradient Boosting Regressor  |  -0.09648  |

- All the model perform poorly on the dataset and are unable to capture the underlying patterns or relationships between the features and the target variable
- The dataset is highly non-linear and contains complex interactions that these linear models cannot effectively capture

Ridge Regression is selected as it outperforms other models

### Hyperparameter Tuning
After conducting hyperparameter tuning with GridSearchCV, the Ridge model was optimized with:
- alpha: 0.1
- solver: saga


## Model Evaluation
### Accuracy
The model achieves an accuracy score of negative 0.21.
  

### Mean Absoluate Error
The mean absolute error (MAE) represents the average magnitude of errors between predicted and actual values, with the model's MAE being 8,280,583.44


### Mean Square Error

The mean squared error (MSE) measures the average squared differences between predicted and actual values, with the model's MSE being 98,895,124,971,391.2

### Root Mean Square Error

The root mean squared error (RMSE) is the square root of the average squared differences between predicted and actual values, with the model's RMSE being 9,944,602.806115044

### R-sqaured 
The R-squared (R2) score quantifies the proportion of the variance in the dependent variable that is predictable from the independent variables. The model R2 is -5832.99670744806. A negative R2 score indicates that the model performs worse than a model that predicts the mean of the target variable for all observations.

## Model Prediction Explanation
When evaluating model performance, it's crucial to consider the context of the dataset. In this case, some of the columns in the dataset consists of random numbers, which inherently lack any meaningful patterns or relationships. Therefore, it's not surprising that the model's performance appears poor.

Since there are no underlying patterns for the model to learn from, any predictive capability observed is likely due to chance rather than true predictive power. It underscores the importance of working with real-world data that contains relevant features and relationships for accurate model training and evaluation.


## Future Improvements
- Explore other models, feature engineering techniques, or data preprocessing methods to potentially improve the model performance
- Rectify potential shortcomings within the existing dataset
- Verify and uphold high standards of data quality throughout the analysis process
- Augment the dataset by acquiring additional data, encompassing both more features and a greater volume of entries

*In machine learning, there's a saying: "Garbage in, garbage out."*

Fin!
