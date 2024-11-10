# Big Mountain Resort Pricing Model
<img src="images/2.jpg?raw=true"/>


## Big Mountain Resort Price Analysis


## Introduction
Big Mountain Resort is a popular ski resort located in Montana, that currently welcomes 350,000 visitors annually. The resort offers fantastic views of the Flathead National Forest and Glacier National Park in addition to several different types of ski runs. It’s services include 11 lifts, 2-T bars, and 1 magic carpet for novice skiers. The base elevation is 4,464 feet, the summit is 6,817 feet, and the longest run is 3.3 miles in length. Big Mountain Resort has recently installed a new chair lift to increase visitors’ distribution across the mountain. This has increased their operating costs by $1.54 million this season. This new cost has caused the business to rethink their pricing strategy, which was previously to charge a slight premium above the average price of resorts in its market segment. But they now suspect that given their facilities and premium positioning, they can make data driven decisions to investigate if a price increase is feasible.
## Problem Statement:
What opportunities exist for Big Mountain Resort to effectively make data-driven decisions about ticket prices and implement a new pricing strategy 
Current Resort's Pricing Strategy:
Big Mountain Resort currently bases their pricing mainly putting a small premium on just the market average. This won’t be enough to maximize their capitalization investment and can’t be sustainable to gain an edge over the competition.
## Modeling scenarios:
Big Mountain Resort has been reviewing potential scenarios for either cutting costs or increasing revenue (from ticket prices). Ticket price is not determined by any set of parameters; the resort is free to set whatever price it likes. However, the resort operates within a market where people pay more for certain facilities, and less for others. Being able to sense how facilities support a given ticket price is valuable business intelligence. This is where the utility of our model comes in.
The business has shortlisted some options:
Permanently closing down up to 10 of the least used runs. This doesn't impact any other resort statistics.
Increase the vertical drop by adding a run to a point 150 feet lower down but requiring the installation of an additional chair lift to bring skiers back up, without additional snow making coverage
Same as number 2, but adding 2 acres of snow making cover
Increase the longest run by 0.2 mile to boast 3.5 miles length, requiring an additional snow making coverage of 4 acres
The expected number of visitors over the season is 350,000 and, on average, visitors ski for five days. Assume the provided data includes the additional lift that Big Mountain recently installed.
## Data Wrangling
Our dataset includes several important values like the total vertical drop, number of lift chairs, weekday/weekend price, and total number of runs for each resort. The first values inspected were the AdultWeekend vs AdultWeekday prices, was it actually advantageous to have a different price for the weekend? Most states had the same price for both, as seen by the chart below: 

<img src="images/Figure1.png?raw=true"/>

Not only did the weekend and weekday values match for every entry in Montana, our resort’s home state, but AdultWeekend had several missing values. Because of this, the AdultWeekend column was removed. In addition to AdultWeekend, the fastEight column was dropped because the value of it’s values were null and the other half were mostly 0. Besides those two big ones, there were some smaller columns that had to be dropped and a lot of missing values that had to be taken care of. Once this was finished we were left with 277 of the original 330 rows. 

## Exploratory Data Analysis								
In order to find trends, patterns, and actionable insights in the data, we need to explore and find these patterns. The first pattern explored was the relationship between the total number of resorts by population vs total number of resorts by area. This didn’t yield much usable information for Big Mountain Resort, but it did clear up some initial thoughts. The next relationship I wanted to look into was the relationship between the components like vertical drop, years open, or skiable areas versus the price in each state. This required a Principal Cumulative Analysis (PCA), which showed that the first two components account for 75% of the variance, and the first four account for 95%. Focusing on just the two components, I scaled the data and added the average ticket price to a scatter plot. I needed to see a more clear relationship between price and components, so instead I created a heatmap to better visualize the relationship between each feature 

<img src="images/Figure2.png?raw=true"/>

## Feature Engineering:
Feature Correlation heatmap: a great way to gain a high level view and identify patterns of relationships amongst the features:
summit and base elevation are quite highly correlated. This isn't a surprise.
AdultWeekend ticket price, we see quite a few reasonable correlations. fastQuads stands out, along with Runs and Snow Making_ac.
The last one is interesting. Visitors would seem to value more guaranteed snow, which would cost in terms of snow making equipment, which would drive prices and costs up.
As well as Runs, total_chairs is quite well correlated with ticket price. This is plausible; the more runs you have, the more chairs you'd need to ferry people to them! Interestingly, they may count for more than the total skiable terrain area. For sure, the total skiable terrain area is not as useful as the area with snow making. People seem to put more value in guaranteed snow cover rather than more variable terrain area.



## Feature Correlation Scatterplots: Correlations, particularly viewing them together as a heatmap, can be a great first pass at identifying patterns. But correlation can mask relationships between two variables
There's a strong positive correlation with vertical_drop.
fastQuads seems very useful. Runs and total_chairs appear quite similar and also useful.

<img src="images/Figure3.png?raw=true"/>

## Pre-Processing and Training Data:
Linear Model: In the process of building the linear model, missing values were imputed with the median and mean values. If ticket prices were predicted using the linear model, they would be off by about $9. However, the initial linear model was overfitting and needed to be adjusted by the number of features. Through cross-validation, the value of k was set to eight features to focus on: vertical_drop, Snow Making_ac, total_chairs, fastQuads, Runs, LongestRun_mi, trams, and SkiableTerrain_ac. These features fit our initial assumptions from EDA.

Random Forest Model: Like the linear model, missing values were imputed with the median and mean values. While imputing the median was helpful, it was not helpful to scale the features. The random forest model revealed that the top four features to consider are fastQuads, Runs, Snow Making_ac, and vertical_drop.

Final Model Selection: After testing both the linear model and random forest model, the project will be moving forward with the forest regression model. Comparison of the two demonstrated that performance on the test set was consistent cross-validation results. Additionally, the cross-validation mean absolute error was lower using the random forest regressor.

<img src="images/Figure4.png?raw=true"/>

## Recommendations:
Our Model suggests that Mountain Resort’s ticket price is lower than the predicted model by 16.31%, and the resort have many potential scenarios for either cutting costs by closing runs or increasing ticket price by increasing vertical drop, adding acres of snow making or increasing the longest run.
Increasing the vertical drop by 150 ft would increase the ticket price by 10.44% from $81 to $95.87.
Adding 2 acres of snow making would increase the ticket price by 12% from $81 to $90.75, resulting in revenue increase by $17,068,841.
When it comes to closing up to 10 used Runs, our Model predicted the following:
Closing one run will have no impact on Ticket price or revenue.
Closing 2 runs reduce support for ticket price and so revenue by $0.4 and $750,000 respectively.
Closing down 3 runs, it seems they may as well close down 4 or 5 as there’s same loss in ticket price and revenue by $0.67 and $1.250M respectively.
Closing 10 runs reduces support for ticket price and so revenue by $1.71 and $3M respectively.
Because we don’t know the operating cost per used run, we can’t determine how much cost saving will offset the loss in revenue after closing more than one run.

<img src="images/Figure5.png?raw=true"/>

## Conclusions
After applying our Model for ski resort ticket price and leverage it to explore Big Mountain Resort’s potential scenarios for increasing revenue, we can conclude that:
The best scenario where we managed to gain the highest revenue increase possible was by increasing the vertical drop by 150 ft, adding one Chair Lift, adding one run and adding 2 acres of snow making cover. This scenario has increased ticket prices by 16.31% from $81 to $95.87.
Due to lack of data in regards of operating cost per used run and weekdays ticket price, our model cannot recommend closing down used runs or implementing a dynamic ticket pricing.
