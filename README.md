[![forthebadge made-with-python](http://ForTheBadge.com/images/badges/made-with-python.svg)](https://www.python.org/) [![ForTheBadge uses-git](http://ForTheBadge.com/images/badges/uses-git.svg)](https://GitHub.com/) [![ForTheBadge built-with-love](http://ForTheBadge.com/images/badges/built-with-love.svg)](https://GitHub.com/rekib0023/)

![Python Version](https://camo.githubusercontent.com/17fa56d1fbad7bb4082c9711a77b984b85e79446/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f507974686f6e2d332e362d627269676874677265656e2e737667) [![Documentation Status](https://readthedocs.org/projects/ansicolortags/badge/?version=latest)](http://ansicolortags.readthedocs.io/?badge=latest) ![Scikit-Learn](https://camo.githubusercontent.com/16820243f022701e81f9f55095b0dc6bb3be986e/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4c6962726172792d5363696b69745f4c6561726e2d6f72616e67652e737667)

# House-Rent-Prediction-Pipeline-Overview
:house_with_garden::house_with_garden::house_with_garden::moneybag::moneybag::heart::heart:


The main objective of the project was to build a regression model that would help us to predict monthly house rent depending upon the various features like the sqfeet, the no. of rooms and bathrooms and so on.


## Table of Contents
- [Data Source](#data-source)
- [Data Description](#data-description)
  - [Statistical Description](#statistical-description)
  - [Target Variable](#target-variable)
  - [Missing Values](#missing-values)
  - [House Type](#house-type)
  - [Correlation](#correlation)
- [Feature Engineering](#feature-engineering)
- [Model Building](#model-building)

## Data Source
For the convenience I have uploaded the dataset to Google Drive. Here is the shared [link](https://drive.google.com/drive/folders/16n1lch7y9iVNdetydfwW7pa2s2Z-AINT?usp=sharing).

## Data Description
The dataset contains 265190 records of house, a huge number of these records are mostly from the United States with few outliers. The dataset has 22 features, features including various urls, the price, the sqfeet, numeber of beds and baths, description, region etc.

Here is a map showing the house records. As we can see most of the houses are from the United States.

![World Map](/plots/world_map.png)

#### Statistical Description
Let's look at the statistical description of our data
 Desc	| price |	sqfeet |	beds |	baths |	lat |	long
  ---|---|---|---|---|---|---
count |	2.651900e+05| 	2.651900e+05| 	265190.000000 |	265190.000000 	|263771.000000 |	263771.000000
mean |	1.227285e+04 	|1.093678e+03 |	1.912414 |	1.483468| 	37.208855 |	-92.398149
std |	5.376352e+06 |	2.306888e+04| 	3.691900 |	0.630208 |	5.659648 |	17.370780
min |	0.000000e+00 |	0.000000e+00 |	0.000000 |	0.000000 |	-43.533300 |	-163.894000
25% 	|8.170000e+02 |	7.520000e+02| 	1.000000 |	1.000000| 	33.508500 |	-104.704000
50% |	1.060000e+03| 	9.500000e+02| 	2.000000 |	1.000000 |37.984900 |	-86.478300
75% |	1.450000e+03 |	1.156000e+03 |	2.000000 |	2.000000 |	41.168400 |	-81.284600
max 	|2.768307e+09 	|8.388607e+06 |	1100.000000 |	75.000000 |	102.036000 |	172.633000

#### Target Variable
The target variable, here price was highly skewed towards the left side with skewness of 514.78 and kurtosis of 265062.43

![Target Distribution](/plots/target_distribution1.png)

The skewness of the data points are resolved after log transformation. Log transformation gave us a skewness of 4.47 and kurtosis of 52.47

![Target Distribution](/plots/target_distribution2.png)

#### Missing Values
The features containing missing values are:
- parking_options (36%)
- laundry_options (20%)
- lat (0.5%)
- long (0.5%)
- description & state (nominal percentage)
![Missing Values](/plots/missing_data.png)

**Impute missing values**

Here's my take on imputing these missing values:

variables | imputation 
--- | ---
parking_options | mode value of the parking_options for the respective house type
laundry_options | mode value of the laundry_options for the respective house type
lat | mode value of the lattitude for the respective house region
long | mode value of the longitude for the respective house region
state | drop records
description | drop records


#### House Type
Percentage description of the various house types in our dataset
![House Type](/plots/house_type.png)

As we can see apartment acquires around 50% of our dataset, followed by house(7.07%) and flat(5.87%)

#### Correlation

![Correlation](/plots/correlation.png)

As we can see, there is no strong correlation among the independent variables with the dependent variables. Therefore, a linear model will perform terribly in this dataset.


## Feature Engineering

While going through the description of few house records, I came across some interesting information as in houses having a pool, a gym nearby, a fireplace or a shopping mall nearby. I think this information will make a few good features. So I went ahead and made these new features.

Also, as our data was not normally distribute. Performed log transformation on numerical data.

And saved the cleaned dataset to a csv.


## Model Building

4 different learning regressors (Linear Regression, Random Forest, Gradient Boosting, and XgBoost) were tested, and we have achieved the best prediction performance using Random Forest, followed by Gradient Boosting, then XgBoost, while Linear Regression achieved the worst performance of the four.

The best prediction performance was achieved with a Random Forest regressor, using all features in the dataset, and resulted in the following metrics:

- Mean Absolute Error (MAE): 0.059128200788923446
- Root mean squared error (RMSE): 0.1717131883398518
- R-squared Score (R2_Score):  0.8746976791953469

![random_forest_plot](/plots/random_forest_plot.png)

![random_forest](/plots/random_forest.png)

The orange line in the graph represents the actual rents. And the cyan circles plotted against actual rents on the x-axis and predicted rent on the y-axis, are the predicted rents.





## References
- [A Simple Tutorial To Data Visualization](https://www.kaggle.com/vanshjatana/a-simple-tutorial-to-data-visualization/data#Bar-Plot): Kaggle notebook by [Vansh Jatana](https://www.kaggle.com/vanshjatana)
- [Outlier Detection Techniques: Simplified](https://www.kaggle.com/rpsuraj/outlier-detection-techniques-simplified): Kaggle notebook by [Suraj RP](https://www.kaggle.com/rpsuraj)
- Towards Data Science blog: [Easy Steps To Plot Geographic Data on a Map — Python](https://towardsdatascience.com/easy-steps-to-plot-geographic-data-on-a-map-python-11217859a2db)
- Plotly documentation: https://plotly.com/python/
- Folium documentation: https://python-visualization.github.io/folium/quickstart.html
- https://github.com/zeglam/Countries-GDP-prediction

![Forks](https://img.shields.io/github/forks/rekib0023/House-Rent-Prediction-Pipeline-Overview?style=social) ![Watchers](https://img.shields.io/github/watchers/rekib0023/House-Rent-Prediction-Pipeline-Overview?style=social)
