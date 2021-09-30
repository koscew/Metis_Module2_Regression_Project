# Stats to Evaluate the Performance of Batters

Chien Yuan Chang

## Abstract
The goal of this project was to use linear regression model to interpret important factors in affecting the performances of the MLB batters for baseball franchises and fantasy sport players to evaluate the batters and for coaches and players to improve the performances. [On-base Plus Slugging Plus (OPS+)](https://www.mlb.com/glossary/advanced-stats/on-base-plus-slugging-plus) was used to represent the overall performance of the batters. I scraped the player data on [Baseball Reference]('https://www.baseball-reference.com/') and downloaded more statcast data from the [Baseball Savant]('https://baseballsavant.mlb.com/'). After refining the model, the Adjusted R-squared of test data was 0.626 and the Mean Absolute Error was 11.963. The barrel batted rate had highest impact, followed by the percentage of some swing stats. The best batting strategy is to hit the pitches inside the zone hard with right angle and not to swing the pitches outside the zone. The result indicated that Statcast was able to well interpret the overall performance of batters and can be a good tool to evaluate the batters. 

## Design
[Statcast](https://www.mlb.com/glossary/statcast) is a high-speed, high-accuracy, automated tool developed to analyze player movements and athletic abilities in Major League Baseball (MLB) and was installed in all thirty MLB stadiums in 2015. Teams started the arms race of data analysis, and Statcast data has replaced traditional metrics. Building a linear regression model would be able to interpret the relationship between the performances of the players and Statcast data and better understand how to use the Statcast data. The baseball franchises and fantasy sport players can use it to evaluate the batters, and coaches and players can adjust the hitting type and improve the performances.

## Data
* The data of the batters who played at least 162 plate appearances in one single season between 2015 and 2019 was used. It included 681 unduplicated players and 1,925 data points.
* 64 features of the stats of standard batting, advanced batting, and ratio batting and the target, [On-base Plus Slugging Plus (OPS+)](https://www.mlb.com/glossary/advanced-stats/on-base-plus-slugging-plus), was scraped on the [Baseball Reference](https://www.baseball-reference.com/)
* 32 features of the Statcast data was downloaded from the [Baseball Savant](https://baseballsavant.mlb.com/) 
* Most of the features were numerical such as accumulated stats, ratio, and percentage except names, the team, and the league.
* 16 features was undertaken to inform the baseline model.
* 9 features was selected into the final model after data engineering and selection.

## Algorithms
*Web-scraping and Data Cleaning*

* Web-scraping the lists and html page address of the batters from 2015 to 2019 on the pages of [Yearly Major League Baseball Standard Batting Stats](https://www.baseball-reference.com/leagues/majors/2019-standard-batting.shtml) from the [Baseball Reference](https://www.baseball-reference.com/) 
* Web-scraping the Stats of Standard Batting, Advanced Batting, and Ratio Batting on the [player page](https://www.baseball-reference.com/players/) of each batter above from the [Baseball Reference](https://www.baseball-reference.com/) and filtering by 162 plate appearances and the years between 2015 and 2019
* Merging with the Statcast data downloaded from the [Baseball Savant](https://baseballsavant.mlb.com/)

*Feature Engineering*

* Polynomial and basic operations were tried on some features.
* NaN data was filled by 0 or the mean.
* Rolling average data was created. 
* The features was standardized before Lasso Regression and Ridge Regression.
* Box cox normalization was used for some features with skewed distribution.
* Final Features:
    * **[Barrel](https://www.mlb.com/glossary/statcast/barrel) Batted%**
    * **Outside the Zone Swing and Miss%**
    * **[SweetSpot](https://www.mlb.com/glossary/statcast/sweet-spot)%** minus **Barrel Batted%**
    * **[Hard Hit%](https://www.mlb.com/glossary/statcast/hard-hit-rate)** minus **Barrel Batted%**
    * **Swing%**
    * **[Sprint Speed](https://www.mlb.com/glossary/statcast/sprint-speed)**(ft/sec)
    * **Z-Swing%** times **Z-Contact%**
    * **Fly Ball%**
    * **Age** minus 17 (minimum age to play in MLB)

*Models*
  
Simple Linear Regression, Lasso Regression, and Ridge Regression were used before settling on Simple Linear Regression as the model since all three models presented similar cross-validation performances.

*Model Evaluation and Selection*
  
The entire training dataset of 1,925 records was split into 80/20 train vs. holdout. Predictions on the 20% holdout were limited to the very end, so this split was only used and scores seen just once.

Metrics/Data|Train Data|5-fold CV|Test Data
---:|---:|---:|---:
R-Squared|0.603|0.598|0.635
Adjust R-Squared|0.601|0.595|0.626
MAE|12.814|12.889|11.963
RMSE|15.957|16.049|15.367

Features|Coefficient|P-Value|
---:|---:|---:|
Constant|-41.53|0.001\*|
Barrel Batted%|6.263|<0.001\*|
Sprint Speed(ft/sec)|3.075|<0.001\*|
Swing%|-1.568|<0.001\*|
Z-Swing% * Z-Contact%|1.563|<0.001\*|
SweetSpot% - Barrel Batted%|1.393|<0.001\*|
Outside the Zone Swing&Miss%|-0.966|<0.001\*|
Hard Hit% - Barrel Batted%|0.658|<0.001\*|
Fly Ball%|-0.522|<0.001\*|
Age - 17|-0.393|0.001\*|


## Tools
* Python BeautifulSoup for web scraping
* Python Pandas and Numpy for data manipulation, data cleaning, data restructuring, exploratory data analysis, and feature engineering
* SQLite3 for managing database and tables
* Python SQLAlchemy for import csv files into tables in SQLite3 database and querying from the database
* Python Matplotlib and Seaborn for data visualization
* Python Statsmodels for linear regression model
* Python Scikit-learn for train/test data splitting, linear regression modeling, cross validation, regularization, metrics  

## Communication
In addition to the slides of the [final presentation](final_presentation.pdf), [charts](images/), [raw data](data/) and this written description, the findings will be posted on [my personal blog](https://koscew.github.io/) in the future.
