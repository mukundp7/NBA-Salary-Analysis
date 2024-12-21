# NBA Salaries SQL/Tableau Data Analysis and Visualization Project

## Overview
This project involved using SQL to perform exploratory data analysis on an NBA dataset which contained player names, age, salary, and stats for each NBA season between 2000-2020. The insights were then visualized using tableau to create a dashboard that effectively conveyed the results. The goal of this project was to show how NBA salaries have changed over time. These insights could be used in further analysis projects to dig deeper into what led to each of the results. 

```sql
```
## Creating The Tables To Store The Datasets
```sql
DROP TABLE IF EXISTS nba_playerstats;
CREATE TABLE nba_playerstats(
	Season INT,
	Player VARCHAR(100),
	Pos VARCHAR(10),
	Age INT,
	Tm VARCHAR(10),
	G INT,
	TRB INT,
	AST INT,
	PTS INT
);
```
```sql
DROP TABLE IF EXISTS nba_playersalaries;
CREATE TABLE nba_playersalaries(
	Player VARCHAR(50),
	Season INT,
	Salary VARCHAR(15)
);
```
