
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

**Evaluation Metric**: We opted for the Root Mean Square Error (RMSE) as our primary evaluation metric. RMSE is particularly suitable for regression problems as it penalizes larger errors more severely, providing a more accurate reflection of the model's performance.


