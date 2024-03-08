# dbt™ Data Modeling Challenge - NBA Edition

# ISTVAN MOZES SUBMISSION

## Table of Contents
1. [Introduction](#introduction)
2. [Data Sources](#data-sources)
3. [Methodology](#methodology)
   - [Tools Used](#tools-used)
   - [Applied Techniques](#applied-techniques)
4. [Visualizations](#visualizations)
   - [Team Playoff Appearances](#team-playoff-appearances)
   - [Player Playoff Games](#player-playoff-games)
   - [Top Playoff Scorers](#top-playoff-scorers)
   - [Top Regular Season Scorers](#top-regular-season-scorers)
   - [NBA Players by University](#nba-players-by-university)
5. [Conclusions](#conclusions)

## Introduction
Explore my project for the _dbt™ data modeling challenge - NBA Edition_, Hosted by [Paradime](https://www.paradime.io/)! This project dives into the analysis and visualization of NBA statistics, designed for basketball enthusiasts and analysts. My analysis focuses mostly on the historical context of how offense and defense has changed in the NBA. I was making an attempt to find a connection between offensive/defensive performance and championships and finally was looking for a correlation between physical parameters and performance. 

### [My GitHub repo](https://github.com/paradime-io/paradime-dbt-nba-data-challenge/tree/nba-istvan-mozes-90-gmail-com)

## Data Sources
My analysis leverages five key NBA datasets from Paradime and one seed file from an external source (NBA.com):
- *stg_games*
- *stg_player_game_logs*
- *stg_team_stats_by_season*
- *stg_teams*
- *stg_common_player_info*
- *NBA_DRAFT_COMBINE_2000_2023_CLEANED.csv*

## Methodology
### Tools Used
- **[Paradime](https://www.paradime.io/)** for SQL, dbt™.
- **[Snowflake](https://www.snowflake.com/)** for data storage and computing.
- **[Sigma](https://app.sigmacomputing.com/paradime-io-nba/workbook/team_stats_by_season-404NCzYBYv9r9Hg7cZHbas)** for data visualization.

### Applied Techniques
- SQL and dbt™ to create _player_advanced_stats_ and _team_advanced_stats_ by transforming _stg_player_game_logs_ and _stg_games_, enriching the box score statistics by calculating advanced statistical metrics, such as _possessions_, _pace_, _offensive_efficiency_, _defensive_efficiency_, offensive_rebound_percentage_, defensive_rebound_percentage_, _free_throw_rate_,  _effective_field_goal_percentage_, _true_shooting_percentage_, _rebound_percentage_, _steal_percentage_, _block_percentage_ and _PER_. To calculate advanced metrics I used the formulas found on [this page](https://www.nbastuffer.com/analytics-101/). 
- SQL and dbt™ to create _stg_draft_combine_ by transforming _NBA_DRAFT_COMBINE_2000_2023_CLEANED.csv_ seed file. I got this data from www.nba.com.
- SQL and dbt™ to transform _team_advanced_stats_ and create _fct_aggregated_metrics_by_reg_szn_ to understand how metrics have changed over time.
- SQL and dbt™ to transform _player_advanced_stats_ and _stg_common_player_info_ to create _fct_aggregated_metrics_by_reg_szn_position_ to see how metrics have changed over time by player position.
- SQL and dbt™ to transform _player_advanced_stats_, stg_common_player_info_ and _stg_draft_combine_ to create _player_average_stats_enriched_ to understand player level statistics, enriched with the players physical parameters such as _height_ and _wingspan_.
- SQL and dbt™ to transform _player_average_stats_enriched_ to understand the connection between game performance and the _height_wingspan_ratio_.
- SQL and dbt™ to transform _player_advanced_stats_ for insights on number of players by season with outstanding individual performances in _fct_nr_of_25_plus_ppg_player_by_reg_szn_ , _fct_nr_of_50_60_point_game_player_by_reg_szn_ and _fct_nr_of_8_plus_3pa_player_by_reg_szn_.
- SQL and dbt™ to transform _player_advanced_stats_ , _stg_teams_ and _team_advanced_stats_ to generate _fct_nr_of_champs_leading_stats_ to see how many championship teams were leading or in top3/top5 in that season in certain statistics.
- SQL and dbt™ to transform _team_advanced_stats_ to see all time ranking in offensive and defensive efficiency on a team level in _fct_team_defensive_efficiency_all_time_reg_szn_ and _fct_team_defensive_efficiency_all_time_reg_szn_ and all time point per game in _fct_team_ppg_all_time_reg_szn_.


## Visualizations

### Historical context of NBA offense
There's a lot off buzz recently that the NBA offense has broken, there is no defense anymore, every other game sets a new record for scoring or individual players score 50-60-70 points. I wanted to find out if it can be statistically proven or it is maybe just recency bias.

#### Points per game by Season

![image](https://github.com/moses90/nba-challange/assets/23437333/82f7fbef-0c7d-48c5-9cd9-72df7508a0a3)

*Insights:* 
We can certainly see an upward trend in the past 25 years and this year is close to the all-time high but it has been higher in the beginning of the 60s. 

### Pace per game by Season

![image](https://github.com/moses90/nba-challange/assets/23437333/d3a2d73d-0f1a-446b-98ef-e022ea960f43)

*Insights:* 
We can see a similar trend in pace too, it had a decline in the end of the 80s but since it has been increasing.

### Offensive Efficiency per game by Season

![image](https://github.com/moses90/nba-challange/assets/23437333/674c0e8d-0ba8-45b9-b293-9e1659643a49)

*Insights:* 
In the offensive efficiency however,  we can definitely see an increase since the 1985-86 season (Based on the data provided, I couldn't sufficiently calculate the offensive efficiency before the 85-86 season). Within this window this year's offensive efficiency is the all-time high. 

### Three point attempts and Three point percentage by Season

![image](https://github.com/moses90/nba-challange/assets/23437333/55494075-c7a6-4524-ad00-c71fd78af1e0)

*Insights:* 
Increasing points and offensive efficiency can be directly connected to three point shooting. Since Mike D'Anthony we know that three point shooting is is more effective than two point shooting, so players started to attempt more and more threes, that's what we can see on this chart too. About 30 years ago there was under 10 three point attempts per game, whereas in recent years it is around 36 attempts per game. In the meantime we can see that three point percentage hasn't changed significantly, the league average was always between 33 and 36%, so it is not a surprise to see an increase in points and offensive efficiency.

### Three point attempts by Position and Season

![image](https://github.com/moses90/nba-challange/assets/23437333/072d2043-2d98-4d70-b12d-75437cd7835f)

*Insights:* 
For the full context of three point shooting, we need to examine the different positions too. We can see here that every position has increased the 3 point attempts, however, forwards and especially centers did it in a bigger proportion. 40 years ago, in the 1983-84 season guards on average attempted 0.43 three pointers per game, in 2023-24 this number is 4.22 which is 9.81 times higher. Forwards in 83-84 attempted 0.14 threes, in 23-24 it was 3.07 attempts which is 21.93 times higher. Centers though, attempted 0.03 three pointers in the 83-84 season, whereas now it is 1.22 which is a 40.67-time increase.

### All-time teams in Points per game 

![image](https://github.com/moses90/nba-challange/assets/23437333/75bc4e83-96de-4413-b62b-30335d9fe810)

*Insights:* 
In the top 20 teams all-time in points per game, 11 is from the past 5 years, in the top 3, 2 is from the 2023-24 season. 

### All-time teams in Offensive Efficiency

![image](https://github.com/moses90/nba-challange/assets/23437333/f874fe23-571b-4885-b979-977c6b358f84)

*Insights:* 
If we check out the same but with offensive efficiency, we see that all top 20 teams are from the past 4 seasons, the top 6 offensive efficiency all-time is from the 2023-24 season.

### 

![image](https://github.com/moses90/nba-challange/assets/23437333/08e5e652-c42f-4f2b-8180-3781ef457129)

*Insights:* 

### 

![image](https://github.com/moses90/nba-challange/assets/23437333/e296624c-c5f1-4250-844b-bc535da2eea2)

*Insights:* 

### 

![image](https://github.com/moses90/nba-challange/assets/23437333/650cb3f9-ec9e-4c32-920d-f62a079a8b24)

*Insights:* 

### Number of players with 25+ point per games by Season

![image](https://github.com/moses90/nba-challange/assets/23437333/eb9c6c38-718f-4c00-9623-218029c5d00b)

*Insights:* 
If we dive even a bit deeper in individual performance we can see the number of players with an average of 25 points or higher is also dominating in the past few years. The 5 most are the last 5 years.

### Number of players with 8+ three point attempts by Season

![image](https://github.com/moses90/nba-challange/assets/23437333/f32557d4-9a7b-4c1f-b256-beb65b850446)

*Insights:* 
Similarly the number of players with an average of 8 or more three point attempts per season shows that 2023-24 season is leading the way with 18 players, and the top 9 places are all seasons after 2015.

### Number of players with 50+/60+ point games by Season

![image](https://github.com/moses90/nba-challange/assets/23437333/b0670cb3-83fc-4c51-aef6-5828c21c189c)

*Insights:*
After all these it is not a surprise to see an increase of the number of outstanding individual performances. The number of 50+ point games by a player was 25 last season and the 2023-24 season is on the 9th place with 13 of them. However, if we see the number of 60+ point games, 2023-24 is again leading the way with 5, which is mind-boggling considering the fact that we have only half season of that for this season.

### defense

![image](https://github.com/moses90/nba-challange/assets/23437333/cd2787a7-4f6a-40a4-a59d-0f130f7860f6)

![image](https://github.com/moses90/nba-challange/assets/23437333/473d57bc-8f49-4602-a16d-a88d809cc137)

![image](https://github.com/moses90/nba-challange/assets/23437333/53309164-e336-4e3c-b2de-7ae26656088e)

*Insights:* 
I'd like to mention as a disclaimer that defense is much harder to measure relevantly than offense, especially with box-score statistics. With modern technologies like motion-tracking there are much more advanced techniques to generate defensive statistics. 

### 

![image](https://github.com/moses90/nba-challange/assets/23437333/156fd84d-34c7-49ff-a98a-57858315b5f2)

*Insights:* 

### 

![image](https://github.com/moses90/nba-challange/assets/23437333/156bc231-e467-46c6-a336-e42c7a690b53)

*Insights:* 

### 

![image](https://github.com/moses90/nba-challange/assets/23437333/122fc080-06cc-45e9-bd69-140c3072f7a9)

*Insights:* 

### 

![image](https://github.com/moses90/nba-challange/assets/23437333/fe620423-2869-4477-a1b0-f0718d2c880b)

*Insights:* 

### 

![image](https://github.com/moses90/nba-challange/assets/23437333/ea47c13a-b479-4ecb-ad2f-8f272e4c78d4)

*Insights:* 

### 

![image](https://github.com/moses90/nba-challange/assets/23437333/0f82a2f4-0eb9-4dca-9906-3290fede359f)

*Insights:* 

### 

![image](https://github.com/moses90/nba-challange/assets/23437333/43122566-eb32-40a6-87cb-96d78a563f80)

*Insights:* 





### Team Playoff Appearances
Visualization of playoff appearances for all 30 NBA teams, including their playoff appearance rates.

![Team Playoff Appearances](https://github.com/paradime-io/paradime-dbt-nba-data-challenge/assets/107123308/cd69a2fa-6b60-44de-b8bc-2f6a6828f033)

*Insights:*
The Los Angeles Lakers' dominance in playoff appearances, and the San Antonio Spurs' highest playoff appearance rate.
The Spurs have only missed the playoffs 9 times!

### Player Playoff Games
Assessment of NBA players with the highest number of playoff game wins and their win percentages. The '*' next to NBA Player name indicates if they're 
a member of the [NBA Greatest 75 Team](https://www.nba.com/news/nba-75th-anniversary-team-announced)

![Player Playoff Games](https://github.com/paradime-io/paradime-dbt-nba-data-challenge/assets/107123308/ffd6abf3-b8a8-411f-a0be-12402a5d1b45)

*Insights:* 
LeBron James has the most playoff wins of any player, but here's what's most interesting: 
Of the 25 players with the most playoff wins, only 12 of them are members of the [NBA Greatest 75 team](https://www.nba.com/news/nba-75th-anniversary-team-announced). 
There are several players listed that impact playoff wins and compliment their team's best players, but aren't known 
as on the the all time greats, such as: Derek Fisher, Robert Horry, Danny Green. 

### Top Playoff Scorers
Showcases players who achieved the the most points scored in any playoff season.

![Top Playoff Scorers](https://github.com/paradime-io/paradime-dbt-nba-data-challenge/assets/107123308/db51f47a-5cfb-431c-9c7b-3a793a6b4352)

*Insights:* 
Michael Jordan, LeBron James, and Kobe Bryant are the only players having three seasons within the top 25 
highest most points scored in a playoff season.

### Top Regular Season Scorers
Highlights NBA players who scored the most in regular seasons.

![Top Regular Season Scorers](https://github.com/paradime-io/paradime-dbt-nba-data-challenge/assets/107123308/774223ad-11f0-4202-817f-5a8c1daf3afc)

*Insights:* 
Wilt Chamberlain is one of the best regular season scorer of all time. In addition to having the most points scored 
in any regular season ever (4,029), he also has six season in the top 25. The only other player with 6 top 25 seasons is Michael Jordan.
In the chart above, notice that Wilt Chamberlain doesn't appear once in the top 25 playoff scorers of all time 👀.

### NBA Players by University
Displays which universities have produced the most NBA players.

![NBA Players by University](https://github.com/paradime-io/paradime-dbt-nba-data-challenge/assets/107123308/e21af17a-9cb8-491a-8e0d-b70eae118324)

*Insights:* 
Kentucky has produced the most NBA players in NBA history by a significant margin.... Go Wildcats! Also, this data is [slightly inaccurate](https://erudera.com/resources/colleges-with-most-nba-players/), but that's the NBA API's fault, not mine 🤣

## Conclusions
This project successfully extracts significant insights from NBA data that NBA fans would find interesting, such as: 

- The dominance of teams like the Los Angeles Lakers and the San Antonio Spurs in playoff appearances
- The critical role of "role" players, as highlighted by the playoff games by player insights,
- The extraordinary achievements of players like LeBron James, Michael Jordan in the playoffs, and Wilt Chamberlain in the regular season. 
- The influence of universities like Kentucky in producing NBA talent.
