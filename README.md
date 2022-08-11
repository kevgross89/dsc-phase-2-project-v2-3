# King County House Sales Data Analysis

![King_County_Logo](https://github.com/kevgross89/dsc-phase-2-project-v2-3/blob/main/Images/King%20County%20Housing%20Logo.jpg)

Author: Kevin Gross

## Project Overview

This project analyzes housing data from King County, Washington to help interpret and predict future house sale prices. The variables used below include number of bedrooms, number of bathrooms, square footage of the living space, square footage of the lot, number of floors, the year the house was built, the numeric grade the house received, the conditional grade the house received, and whether or not the house was touching the water. 

![Map](https://github.com/kevgross89/dsc-phase-2-project-v2-3/blob/main/Images/KC%20Map.jpg)

## Business and Data Understanding

**The stakeholder for this project is Berkshire Hathaway's clients, also known as their home buyers and home sellers. Berkshire Hathaway's goal is to use the data provided below to provide advice to their clients on how to increase the value of their home.** The regression analysis starts off at a basic level with 1 dependent variable predicting the price of a home and then builds using multiple iterations of linear regression. 

## Modeling

This project uses linear regression to formulate a baseline model to predict King County housing prices. From there, additional numeric variables are added into the model to help increase the r-squared value, which is the percentage of variation explained by the relationship between the dependent variable(s) and the independent variable (housing price). A third linear regression model is then created using categorical variables.

After all of the statistically significant variables have been added into our linear regression model, we look to remove some of the coefficients to simplify our model to avoid overfitting. Even though some of these variables are statistically significant, we can remove them from our model with a minimal effect on the r-squared score.

Last but not least, we have to log some of our variables in order to meet the 4 linear regression assumptions: linearity, multicollinearity, normality, and homoscedasticity. 

## Regression Results

![Heatmap](https://github.com/kevgross89/dsc-phase-2-project-v2-3/blob/main/Images/Correlation_Heatmap.png)

The most correlated feature to predict our independent variable, price, turned out to be the **square footage of the house** which had a 0.7 Pearson Correlation Coefficient between the two variables. This suggests that there is a significant positive relationship between the square footage and price, meaning that generally speaking, as the square footage of the house increases, so does the price of the house. This baseline model gives us a 0.49 r-squared value which means that roughly half of the variation in the data can be explained by our model. The simplest way to interpret this model is below:

* Predicted House Price = Square Footage of House * 283 - $47,945

![Ft_V_Price](https://github.com/kevgross89/dsc-phase-2-project-v2-3/blob/main/Images/Square_Ft_v_Price.png)

Obviously, this model has some flaws as it is possible (although not probable) that it would predict a negative house price if a house had less than 170 square feet.

Our second linear regression model adds in significantly more coefficients to help better predict the house price. For the second model, we add in the variables of bedrooms, bathrooms, square footage of the lot, number of floors, the year the house was built and the numeric grade the house received (index from 1 to 13, where 1-3 falls short of building construction and design, 7 has an average level of construction and design, and 11-13 have a high quality level of construction and design). **This second model gives us an r-squared value of 0.614, which is a 12% improvement from our baseline model.** The simplest way to interpret this model is below:

* Predicted House Price = (Square Footage of House * 191) - (Number of Bedrooms * 48454) + (Number of Bathrooms * 51156) - (Square Footage of Lot * .24) + (Number of Floors * 17181) - (Year Built * 4171) + (Numeric Grade * 132477) + $7,382,644

The third linear regression model adds in categorical features, such as whether the house is a waterfront property or not. **Our r-squared model increased to 0.644, which is a 3% improvement from our second model above.** While this model is the most accurate in predicting a house price, it is also complicated to understand.

* Predicted House Price = (Square Footage of House * 180) - (Number of Bedrooms * 42312) + (Number of Bathrooms * 46440) - (Square Footage of Lot * .22) + (Number of Floors * 21534) - (Year Built * 3835) + (Numeric Grade * 131265) - (Fair Condition (Y/N) * 2698) + (Good Condition (Y/N) * 13468) + (Poor Condition (Y/N) * 12326) + (Very Good Condition (Y/N) * 51646) + (Waterfront (Y/N) * 780006) + $6,723,548

The fourth model aims to keep the r-squared score as high as possible, while also simplifying the model. This model decreases the number of dependent variables from 13 to 7, while keeping our r-squared score at 0.642 which is only a 0.2% decrease in the amount of variation explained by our model. 

* Predicted House Price = (Square Footage of House * 175) - (Number of Bedrooms * 41073) + (Number of Bathrooms * 54699) - (Year Built * 3929) + (Numeric Grade * 133251) + (Waterfront (Y/N) * 779549) + $6,917,330

Unfortunately, while this model is the most accurate, it also does not meet the 4 assumptions of linear regression. To fix this issue, we can log and standardize some of our features in order to normalize our regression results. After applying these transformations, we have a model that comes back with a r-squared value of 0.634 and meets all 4 assumptions of linear regression.

![Tornado](https://github.com/kevgross89/dsc-phase-2-project-v2-3/blob/main/Images/Tornado.png)

## Business Recommendations

When Berkshire Hathaway is talking to it's clients, it should recommend that clients do the below 2 things to their homes:

* The best way to increase the value of one's home is to increase the Numeric Grade. This is indicated by an index from 1 to 13, where 1-3 falls short of building construction and design, 7 has an average level of construction and design, and 11-13 have a high quality level of construction and design. Since this is on a scale of 1 to 13, **if we increase our Numeric Grade by 1 notch (1/13 = 7.69%), we would expect the value of our home to increase by 4.2%** (formula: (1.0769<sup>0.5511</sup> - 1) * 100 = 4.2%).
* Another way to increase the value of one's home is to increase the square footage of the house. **If we increase the square footage of the house by 20%, we could expect the value of the home to increase by 6.2%** (formula: (1.2<sup>0.3318</sup> - 1) * 100 = 6.2%).

## Conclusion

Berkshire Hathaway can use this final model to help their customers predict the price of their home and also forecast the price of a home they intend to purchase. It should explain roughly 63% of the normal variation that happens in everyday life, which means that it is a relatively strong model. 