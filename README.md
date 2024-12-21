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
## Data Analysis
1.) Creating a View for data between the year 2000-2020.
```sql
CREATE VIEW nba_playersalaries_1 AS
SELECT DISTINCT ON (player, season)*
FROM nba_playersalaries
WHERE season BETWEEN 2000 AND 2020;
```

2.) Performing a join to get stats with salary 
```sql
CREATE VIEW nba_playersalaries_stats AS
SELECT 
	nba_playersalaries_1.player,
	nba_playersalaries_1.season,
	nba_playersalaries_1.salary,
	nba_playerstats.pos,
	nba_playerstats.age,
	nba_playerstats.tm,
	nba_playerstats.g,
	nba_playerstats.trb,
	nba_playerstats.ast,
	nba_playerstats.pts
FROM nba_playersalaries_1
JOIN nba_playerstats
ON nba_playersalaries_1.player = nba_playerstats.player AND nba_playersalaries_1.season = nba_playerstats.season;
```
3.) Checking for duplicates
```sql
SELECT 
	*,
    COUNT(*) AS duplicate_count
FROM 
    nba_playersalaries_stats
GROUP BY 
    player, 
    season,
	salary,
	pos,
	age,
	tm,
	g,
	trb,
	ast,
	pts
HAVING 
    COUNT(*) > 1;
```

4.) Creating a View for total stats for each player in a season
```sql
CREATE VIEW nba_playersalaries_totalstats AS
SELECT 
    player, 
    season, 
    MAX(salary) AS salary,  -- Keeps the maximum salary (or adjust as needed)
    MAX(pos) AS pos,        -- Keeps one position (adjust logic as needed)
    MAX(age) AS age,        -- Keeps the maximum age
    MAX(tm) AS tm,          -- Keeps one team (adjust if needed)
    SUM(g) AS total_games, 
    SUM(trb) AS total_rebounds, 
    SUM(ast) AS total_assists, 
    SUM(pts) AS total_points
FROM 
    nba_playersalaries_stats
GROUP BY 
    player, season;
```
5.) Finding the youngest and oldest player in our dataset.
```sql
SELECT 
    MIN(age) AS min_value, 
    MAX(age) AS max_value
FROM 
    nba_playersalaries_totalstats;
```



