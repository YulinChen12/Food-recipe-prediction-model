
# Calories-Prediction-Model 2023
By Yulin Chen & Jiarui Zha  

Exploratory data analysis on this dataset can be found

https://yulinchen12.github.io/Recipe-and-Average-Rating-Research-Project-2023/

# Introduction  
In the realm of culinary arts and nutritional science, understanding the caloric content of food is fundamental. It informs dietary choices, aids in health management, and fuels gastronomic creativity. This project leverages the power of data analysis and machine learning to address a compelling question: Can we accurately predict the calorie count of a recipe based on its inherent characteristics? 

Our primary objective is to develop a predictive model capable of estimating the caloric content of recipes. This model aims to assist dietitians, culinary enthusiasts, and the general public in gauging the nutritional value of different recipes, fostering informed dietary choices. The ability to predict calorie counts from readily available recipe information could transform how we approach cooking and dietary planning.

Our approach encompasses several key stages:

1. Data Collection and Cleaning: Utilizing a dataset of recipes and user interactions, we meticulously clean and preprocess the data, ensuring a robust foundation for our analysis.

2. Feature Engineering: We derive insightful features from the data, focusing on those that are available before the recipe is prepared.

3. Predictive Modeling: Employing machine learning techniques, we build and refine models to predict caloric content. Our journey begins with a baseline model, which we iteratively improve to achieve enhanced accuracy.

4. Fairness Assessment: We conduct a fairness analysis to evaluate whether our model's performance is equitable across different recipe categories, ensuring ethical and unbiased results.

## Framing the Problem

### Data Preparation and Cleaning

The foundation of our analysis lies in the thorough and meticulous data cleaning process. We started by revisiting the data cleaning methods employed in our exploratory data analysis project, ensuring consistency and reliability in our dataset. Our dataset comprises two primary sources: recipe details and user interactions. We merged these datasets to create a comprehensive view of each recipe, including user ratings and comments.

Key cleaning steps included:

1. **Handling Missing Values**: We filled missing ratings with a default value of 0 and addressed other null values appropriately.

2. **Feature Engineering**: We derived new features such as average ratings, preparation times, and counts of specific ingredients or tags (like 'health' mentions in reviews).

### Prediction Problem Definition

**Type of Problem**: We are tackling a regression problem where the continuous response variable is the 'calories' of a recipe.

**Response Variable**: The chosen response variable is the caloric content of each recipe. This variable is pivotal for anyone monitoring their calorie intake or seeking to understand the nutritional value of different recipes.

**Evaluation Metric**: We opted for the Root Mean Square Error (RMSE) and R^2 (Coefficient of determination) as our primary evaluation metric. RMSE is particularly suitable for regression problems as it penalizes larger errors more severely, providing a more accurate reflection of the model's performance.

## Baseline Model

In the initial phase of our predictive analysis, we developed a baseline model to estimate the caloric content of recipes. This model serves as a foundation for our predictive task, setting a benchmark against which we can measure subsequent improvements.

### Features Used:

**Quantitative Features**: We selected three features from our dataset to train our baseline model: **'minutes'**(preparation time), **'n_ingredients'** (number of ingredients), and **'n_steps'** (number of steps in the recipe).

1. 'minutes' (Preparation Time): Preparation time is often correlated with the complexity and style of a recipe. Typically, more elaborate dishes require longer preparation times and can imply a higher likelihood of calorie-dense ingredients. This feature provides a foundational understanding of the recipe's nature.

2. 'n_ingredients' (Number of Ingredients): The number of ingredients serves as a proxy for recipe complexity. Recipes with more ingredients may have a greater variety of food components, including those contributing to higher calorie counts. This feature helps in capturing the diversity within a recipe.

3. 'n_steps' (Number of Steps): Similar to the number of ingredients, the number of steps can indicate a recipe's complexity. More steps might involve processes that add or modify caloric content, such as frying or adding sauces.

**Feature Transformation**: We applied StandardScaler from sklearn to these features, ensuring they are appropriately scaled for use in our regression model.

### Model Choice

The model chosen for this task is a **Decision Tree Regressor**.
We selected the Decision Tree Regressor for our baseline model due to its:

Interpretability: Decision trees provide clear, logical decision paths, making it easy to understand and explain how recipe features influence caloric predictions.

Handling of Non-Linear Relationships: They are capable of capturing complex, non-linear relationships between features and the target variable, which is essential for the diverse nature of recipe data.

Ease of Use with Mixed Data Types: Decision trees effortlessly manage both numerical and categorical data, aligning well with our varied dataset features.

Flexibility: They offer tunable parameters to control model complexity, crucial for preventing overfitting and refining model performance.


### Model Training

**Pipeline Implementation**: We implemented the feature transformations and model training steps in a single sklearn Pipeline. This streamlined approach ensures a more efficient and error-free process in both training and predicting.

**Data Splitting**: We split our dataset into training and test sets, with 35% of the data reserved for testing. This split allows us to evaluate our model’s performance on unseen data, providing insights into its generalization capabilities.

### Performance Evaluation

Metrics Used: To evaluate our model, we used metrics such as Root Mean Square Error (RMSE), Mean Squared Error (MSE), and R^2 Score for both training set and test set. These metrics provide a comprehensive view of the model's accuracy and predictive power.

| Metric    |   Training Set |      Test Set |
|:----------|---------------:|--------------:|
| RMSE      |     424.18     |    416.131    |
| MSE       |  179928        | 173165        |
| R^2 Score |       0.477754 |      0.478437 |

Model Performance:

The R^2 scores close to 0.48 for both training and test sets imply that nearly half of the variance in the calorie content is explained by the model. While this is a reasonable start, there is substantial room for improvement.

General Assessment: While the baseline model establishes an initial understanding of the relationship between recipe characteristics and caloric content, there is room for improvement. The Decision Tree Regressor, in its current form, may not capture all the nuances and complexities of the data.

Areas for Improvement: The model's performance, particularly in terms of RMSE and R^2 Score, suggests that additional feature engineering, more sophisticated modeling techniques, or hyperparameter tuning could yield better results.

## Final Model

### Introduction to Enhanced Features

In refining our predictive model, we focused on incorporating features that provide deeper insights into the factors influencing a recipe's caloric content. These enhancements were guided by culinary intuition and data-driven hypotheses.

#### New Feature Selection and Justification

**Categorical Features** - **'desserts', 'cheese', 'oven', 'health'**:

**Desserts**:

Rationale: Dessert recipes are often characterized by high sugar content, which significantly contributes to calorie density. Including this feature helps the model identify recipes that are likely to be higher in calories due to their dessert classification.

Data Generating Perspective: The dessert categorization is a proxy for recipes rich in sugars and fats, which are key factors in caloric computation. This classification reflects common dietary knowledge where desserts are generally considered calorie-heavy.

**Cheese**:

Rationale: Cheese is calorically dense, rich in fats and proteins. Its presence or prominence in a recipe can be a strong indicator of higher caloric content.

Data Generating Perspective: From a nutritional viewpoint, cheese's high fat and protein content make it a significant contributor to a recipe's total calories. This feature allows the model to adjust predictions upwards for recipes with cheese, aligning with nutritional principles.

**Oven Usage**:

Rationale: The use of an oven is often associated with certain types of recipes, like baked goods, which can vary significantly in calorie content. This feature helps in distinguishing between cooking methods that might correlate with different calorie levels.
Data Generating Perspective: Oven usage can imply certain cooking processes like baking, which is often associated with specific food categories (e.g., baked desserts, casseroles) that have distinct caloric profiles. This differentiation is vital for a nuanced understanding of calorie estimation.

**Quantitative Feature** - **High-Calorie Ingredient Count**:

Rationale: This feature directly addresses the influence of specific ingredients known for their high-calorie content. By counting these ingredients, the model gains a more accurate gauge of the recipe's potential calorie count.

Data Generating Perspective: The count of high-calorie ingredients like fats, oils, sugars, and certain proteins is a straightforward, quantifiable measure of a recipe's calorie potential. This feature is grounded in the fundamental principle of nutrition science that certain ingredients disproportionately contribute to the overall calorie count.

### Pipeline Transformations for all the Features:

**StandardScaler** for Numerical Features:

Applied To: 'minutes', 'n_ingredients', and 'n_steps'.

Purpose: StandardScaler normalizes these numerical features, ensuring they have a mean of 0 and a standard deviation of 1. This scaling is crucial because it removes the bias that could be introduced by the varying scales and distributions of these numerical features. Standardization makes the model more stable and ensures that features with larger scales don’t dominate the model's learning process.

**OneHotEncoder** for Categorical Features:

Applied To: 'desserts', 'cheese', and 'oven'.

Purpose: OneHotEncoder transforms these categorical variables into a format that can be effectively used by the regression model. Since machine learning models require numerical input, OneHotEncoding converts categorical data into a binary matrix, representing the presence or absence of a category with 1s and 0s. This method is particularly useful for nominal categories without intrinsic order, allowing the model to utilize these features without assuming any order or priority.

**Passthrough** for High-Calorie Ingredient Count:

Applied To: 'high_calories_count'.

Purpose: The 'passthrough' strategy is used for the high-calorie ingredient count feature. Since this feature is already numerical and represents a direct count, it doesn't require scaling or normalization. It’s a straightforward quantitative representation of the presence of high-calorie ingredients in a recipe, and its raw value is directly relevant to the model.

### Model Algorithm

The initial baseline model employed a Decision Tree Regressor. For the final model, we continued with the Decision Tree Regressor. The decision to stick with the same algorithm was strategic, as it allows for a direct comparison between the baseline and final models. However, the final model differs significantly in its complexity and sophistication, primarily due to the introduction of new features and advanced hyperparameter tuning.

### Hyperparameter Tuning

In the baseline model, the Decision Tree Regressor was likely used with default parameters. 

**Advanced Tuning**: 

The final model involved a comprehensive hyperparameter tuning process using GridSearchCV. This method systematically explores a range of parameter combinations to find the most effective settings.

**Parameters Tuned**: 

Parameters such as '**max_depth**', '**min_samples_split**', and '**min_samples_leaf**' were among those tuned. These parameters are crucial in controlling the complexity of the tree, balancing between capturing sufficient detail in the data (depth and split) and avoiding overfitting (leaf size).

### Reasoning Behind Tuning:

**Max Depth**: Adjusting 'max_depth' helps in determining how deep the tree should grow. A deeper tree can capture more details but risks overfitting. A shallower tree might generalize better but could underfit.

**Min Samples Split**: This parameter dictates the minimum number of samples required to split a node. Tuning it helps in determining the necessary sample size to consider a split, affecting the granularity of the tree.

**Min Samples Leaf**: Setting the minimum samples for a leaf node helps in controlling the size of the tree's leaves. A larger number prevents the model from creating leaves with very few samples, which can reduce overfitting.

The optimal hyperparameters we found were a **max_depth = None** , **decision_tree__min_samples_leaf': 2**, 
**decision_tree__min_samples_split': 5.**

### Model Improvement 

#### Baseline Model

| Metric    |   Training Set |      Test Set |
|:----------|---------------:|--------------:|
| RMSE      |     424.18     |    416.131    |
| MSE       |  179928        | 173165        |
| R^2 Score |       0.477754 |      0.478437 |

#### Final Model
| Metric    |   Training Set |      Test Set |
|:----------|---------------:|--------------:|
| RMSE      |     295.912    |    319.708    |
| MSE       |   87563.7      | 102213        |
| R^2 Score |       0.736122 |      0.712551 |

**RMSE** (Root Mean Square Error):

Baseline Model: The baseline model had an RMSE of 424.18 on the training set and 416.131 on the test set. These figures represent the standard deviation of the prediction errors, indicating the average distance between the predicted values and the actual values.

Final Model: The RMSE of the final model is lower than these values, it indicates a significant improvement. A lower RMSE means the prediction errors are smaller, and the model's predictions are closer to the actual data.

**R^2 Score**:

Baseline Model: The R^2 scores of 0.477754 for the training set and 0.478437 for the test set in the baseline model.

Final Model: The R^2 scores of 0.736122 for the trainning set and 0.712551 for the test set. An increase in the R^2 score in the final model would mean it can explain a higher proportion of the variance in the target variable.It suggests that the final model, with its advanced features and optimized hyperparameters, captures the underlying patterns in the data more effectively.

## Fairness Analysis

In order to understand our predictive model deeper, we pose the question, “Does our model exhibit differential performance for recipes containing cheese compared to those without?” 

**Group X**: Recipes that include 'cheese'.

**Group Y**: Recipes that do not include 'cheese'.

The metric to test this evaluation is the **RMSE** (Root Mean Squared Error ), since it could give us the model's accuracy by quantifying the average of the prediction errors. Our hypothesis is as follows:

**Null Hypothesis (H0)**: There is no significant difference in the RMSE between recipes with cheese and without cheese .

**Alternative Hypothesis (H1)**: There is a significant difference in the RMSE between recipes with cheese and without cheese.

We firstly set our significance level as the common significance level 0.05. Then we conduct A **permutation test** with 1000 permutations to assess the significance of the difference in RMSE between the two groups. The result shows that the p-value from the permutation test is **0.07**.  

Since p_value ≥ 0.05, we fail to reject the null. we could conclude that there is not enough statistical evidence to reject the null hypothesis, implying that any observed differences in RMSE between the two groups might be due to chance. This outcome does not align with our first thought that calories have to be highly correlated to the “Cheese” feature. However, the test result does not imply absolute certainty. There are no confirmed casual relationships since it can be influenced by various factors. 

## Conclusion

