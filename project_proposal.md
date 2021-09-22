### Project Proposal of Regression project
Chien Yuan Chang
#### Question/need:
I am going to build a linear regression model to interpret the factors of the performances of the hitters in the MLB and/or predict the performances in the coming year. The On-base Plus Slugging Plus (OPS+) will be used as the label.

The baseball franchises and fantasy baseball players can use this model to evaluate the hitters for next year, and the coach can use the result to help the hitters adjust batting types and improve their performances.

>* What is the framing question of your analysis, or the purpose of the model/system you plan to build? 
>* Who benefits from exploring this question or building this model/system?

#### Data Description:
* Dataset: 
  * I will use the players data of the hitters who played more than 162 plate appearances in at least one single season between 2015 and 2019
 
  * Rationality: 
      *  Each MLB team normally plays 162 games per year so 162 plate appearances will be at least one plate appearance per game
      *  The data of EV and HardH% have been recorded only since 2015
      *  Each MLB team only played 60 games in 2020 season due to the pandemic
  * Data size: 
      * There were about 350 hitters over 162 plate appearances per year so there would be 682 unduplicated players with 2,122 data points within 5 years
  * Data source:
      * Scraping the lists and stats of the hitters from 2015 to 2019 on the pages of [Yearly Major League Baseball Standard Batting Stats](https://www.baseball-reference.com/leagues/majors/2019-standard-batting.shtml) from the [Baseball Reference](https://www.baseball-reference.com/) 
      * Scraping the Stats of Standard Batting, Advanced Batting, and Ratio Batting on the [player page](https://www.baseball-reference.com/players/) of each hitter who played more than 162 plate appearances in at least one single MLB season between 2015 and 2019 from the [Baseball Reference](https://www.baseball-reference.com/) 
 
* An individual sample/unit (total 64 columns):

	Html\_id,Name,Year,Age,Tm,Lg,G,  
	PA,AB,R,H,2B,3B,HR,RBI,SB,CS,BB,SO,BA,OBP,SLG,  
	OPS,OPS+,TB,GDP,HBP,SH,SF,IBB,Pos\_Summary,Awards,  
	rOBA,Rbat+,BAbip,ISO,HR%,SO%,BB%,EV,HardH%,  
	LD%,GB%,FB%,GB/FB,Pull%,Cent%,Oppo%,  
	WPA,cWPA,RE24,RS%,SB%,XBT%,XBH%,X/H%,SO/W,  
	AB/SO,AB/HR,AB/RBI,GO/AO,IP%,HR/FB,IF/FB
	
	/players/a/abreujo02.shtml,José Abreu,2015,28,CHW,AL,154,  
	668,613,88,178,34,3,30,101,0,0,39,140,0.29,0.347,0.502,  
	0.85,135,08,16,15,0,1,11,*3D,MVP-21,  
	0.366,135,0.333,0.212,4.50%,21.00%,5.80%,91.8,47.30%,  
	28.10%,48.50%,16.50%,2.95,23.80%,51.50%,24.70%,  
	2.2,0.70%,40.2,29%,33%,10.00%,38%,3.59,  
	4.4,20.4,6.1,1.32,66%,14.20%,13% 

* Expected characteristics/features to work with (total 24 columns):
  * [OPS+](https://www.mlb.com/glossary/advanced-stats/on-base-plus-slugging-plus): On-base Plus Slugging Plus, ([OPS](https://www.mlb.com/glossary/standard-stats/on-base-plus-slugging) / league OPS, adjusted for park factors) x 100
  * Age: Player’s age at midnight of June 30th of that year
  * Player Years: The number of years that the player had played 
  * PA: Plate Appearances
  * Cumulative PA: The number of plate appearances that the player had played
  * BAbip: Batting Avg. on Balls in Plays, (Hits - Home Runs)/(At Bats - SO - HR + Sac Flies)
  * HR%: Home Run Percentage, percentage of all plate appearances a home run was hit, (HR)/(all plate appearances)
  * SO%: Strikeout Percentage, percentage of all plate appearances ending with a Strikeout, (SO)/(all plate appearances)
  * BB%: Base on Balls Percentage, percentage of all plate appearances ending with a Base on Balls, (BB)/(all plate appearances)
  * EV: Average Exit Velocity which is the average speed of the ball off the bat for balls put into play, measured in miles per hour
  * HardH%: Hard Hit Rate, percent of balls in play with an exit velocity of 95 mph or more
  * LD%: Line Drive Percentage, percentage of all balls put into play (including home runs) that are line drives
  * GB%: Ground Ball Percentage, percentage of all balls put into play (including home runs) that are ground balls
  * GB/FB: Ground Ball to Fly Ball Ratio
  * Pull%: Pull Percentage, percentage of all balls put into play (including home runs) that are hit to the batter's pull side
  * Cent%: Center Percentage, percentage of all balls put into play (including home runs) that are hit to the center of the field
  * Oppo%: Opposite-Field Percentage, percentage of all balls put into play (including home runs) that are hit to the batter's opposite (push) side
  * XBT%: Extra Bases Taken Percentage, percentage of times the runner advanced more than one base on a single or more than two bases on a double, when possible
  * SO/W: Strikeout to Base on Balls Ratio
  * GB/FB: Ground Ball to Fly Ball Ratio, includes line drives as fly balls
  * GO/AO: Ground Outs to Air Outs, double plays count as two
  * IP%: Balls In-Play Percentage, percentage of all plate appearances with ball put into play, (AB-SO-HR+SF)/(all plate appearances)
  * HR/FB: Percentage of Fly Balls that were Home Runs, includes all fly balls to the outfield including line drives
  * IF/FB: Percentage of Fly Balls that were on the infield, includes Line Drives


>* What dataset(s) do you plan to use, and how will you obtain the data?
>* What is an individual sample/unit of analysis in this project? What characteristics/features do you expect to work with?

#### Tools:
* Python BeautifulSoup and/or Selenium for web scraping
* SQLite3 for creating database and table and importing csv into table
* Python SQLAlchemy for querying from the database into Python
* Python Pandas for data clean, data restructuring, and exploratory data analysis
* Python Matplotlib, Seaborn and/or Plotly for data visualization
* Python Scikit-learn for linear regression model
* Other Python libraries if needed

>* How do you intend to meet the tools requirement of the project? 
>* Are you planning in advance to need or use additional tools beyond those required?

#### MVP Goal:
* Data visualization of the feature correlation

>* What would a minimum viable product (MVP) look like for this project?