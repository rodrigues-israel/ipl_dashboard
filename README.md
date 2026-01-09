# 📊 IPL SQL Analysis Project
This project contains a set of SQL queries performed on an IPL (Indian Premier League) dataset to extract meaningful batting insights across seasons, players, and teams.

## **Dataset Used**
Table Name: all_season_batting_card

Key Columns Used:
- fullName
- season
- runs
- ballsFaced
- fours
- sixes
- match_id
- current_innings (team)


## **SQL Queries & Insights**

### 1. Top 10 Run-Scorers Overall

```sql
SELECT fullName,SUM(runs) as 'Total_Runs' FROM all_season_batting_card
GROUP BY fullName
ORDER BY Total_Runs DESC LIMIT 10;
```

### 2. Most Runs in a Single IPL Season

```sql
SELECT season, fullName, SUM(runs) as 'Total_Runs' FROM all_season_batting_card
GROUP BY fullName,season
ORDER BY Total_Runs DESC LIMIT 1;
```

### 3. Highest Strike Rates in a Season (Min 100 balls)

```sql
SELECT season, fullName, SUM(ballsFaced) as 'Balls_Faced', (SUM(runs)/SUM(ballsFaced)*100) as 'Strike_rate' FROM all_season_batting_card
GROUP BY fullName,season
HAVING Balls_Faced >= 100
ORDER BY Strike_rate DESC LIMIT 10;

```

### 4. Most Sixes by Player

```sql
SELECT fullName, SUM(sixes) as 'Total_sixes' FROM all_season_batting_card
GROUP BY fullName
ORDER BY Total_sixes DESC LIMIT 1;
```

### 5. Team Aggregate Runs per Season

```sql
SELECT season,current_innings, SUM(runs) as 'Total_runs' FROM all_season_batting_card
GROUP BY current_innings,season
ORDER BY current_innings,Total_runs DESC;
```

### 6. Top 10 Average Runs per Match per Player

```sql
SELECT fullName,AVG(runs) as 'Average_runs_per_match' FROM all_season_batting_card
GROUP BY fullName
ORDER BY Average_runs_per_match DESC LIMIT 10;
```

### 7. Head-to-Head: AB de Villiers & Chris Gayle Runs Compared

```sql
SELECT fullName,SUM(runs) as 'Total_runs' FROM all_season_batting_card
WHERE fullName = "AB de Villiers" OR fullName = "Chris Gayle"
GROUP BY fullName;
```

### 8. Most Fours Hit by Team in a Season

```sql
SELECT season, current_innings as "team_name",SUM(fours) as 'Total_fours' FROM all_season_batting_card
GROUP BY season, current_innings
ORDER BY Total_fours,season DESC LIMIT 10;
```

### 9. Most Matches Played per Player (Top 10)

```sql
SELECT fullName, COUNT(DISTINCT match_id) as "Total_matches" FROM all_season_batting_card
GROUP BY fullName
ORDER BY Total_matches DESC LIMIT 10;
```

### 10. Players with Most 100+ Scores

```sql
SELECT fullName,COUNT(DISTINCT match_id) as "Total_100s" FROM all_season_batting_card
WHERE runs >= 100
GROUP BY fullName
ORDER BY Total_100s DESC LIMIT 5
```