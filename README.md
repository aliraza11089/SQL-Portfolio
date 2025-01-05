# SQL Portfolio

## Overview
This repository contains a collection of SQL queries designed to analyze and gain insights from match and division data. The queries cover a wide range of topics, including division counts, matches per division, teams' performance statistics, and match outcomes. The data comes from a football league, with the primary focus on understanding the structure of divisions, teams' participation, and match results.

## Projects

### 1. Division and Match Analysis

This project includes SQL queries that answer important business and sports-related questions based on divisions and matches in a football league.

#### SECTION #1: Division Counts and Distribution

1. **Which countries have the most divisions, and what is the count of divisions per country?**
   ```sql
   SELECT country, COUNT(*) as Division_per_country
   FROM divisions
   GROUP BY country
   ORDER BY Division_per_country DESC;

2. **What is the count of divisions per country, ordered by the number of divisions?**
   ```sql
   SELECT country, COUNT(*) as Division_per_country
   FROM divisions
   GROUP BY country
   ORDER BY Division_per_country;

3. **Which country has the most divisions, and how many divisions does it have?**
   ```sql
   SELECT country, COUNT(*) as Division_per_country
   FROM divisions
   GROUP BY country
   ORDER BY Division_per_country DESC
   LIMIT 1;

4. **Which divisions belong to the country with the most divisions?**
   ```sql
   SELECT country, division
   FROM divisions
   WHERE country = (SELECT country
                 FROM divisions
                 GROUP BY country
                 ORDER BY COUNT(*) DESC
                 LIMIT 1);

5. **Which countries have exactly one division?**
   ```sql
   SELECT country, COUNT(*) AS Division_per_country
   FROM divisions
   GROUP BY country
   HAVING COUNT(*) = 1;

6. **How many countries have exactly one division?**
   ```sql
   SELECT COUNT(*) as one_division_countries
   FROM (SELECT COUNT(*) FROM divisions
      GROUP BY country
      HAVING COUNT(*) = 1);

7. **Which matches do not have a corresponding division?**
   ```sql
   SELECT divisions.division, matchs.Div
   FROM divisions
   RIGHT JOIN matchs
   ON divisions.division = matchs.Div
   WHERE divisions.division IS NULL
   GROUP BY matchs.Div;

8. **How many matches are there per division?**
   ```sql
   SELECT division, COUNT(*) AS matchs_per_division
   FROM divisions
   LEFT JOIN matchs
   ON divisions.division = matchs.Div
   GROUP BY division;

9. **How many matches are there per division in Belgium?**
    ```sql
    SELECT country, COUNT(*) AS matchs_per_division
    FROM divisions
    LEFT JOIN matchs
    ON divisions.division = matchs.Div
    WHERE country = "Belgium";

10. **How many matches are there per country?**
    ```sql
    SELECT country, COUNT(*) AS matchs_per_division
    FROM divisions
    LEFT JOIN matchs
    ON divisions.division = matchs.Div
    GROUP BY country;

11. **Which country has the most matches per division?**
    ```sql
    SELECT country, COUNT(*) AS matchs_per_division
    FROM divisions
    LEFT JOIN matchs
    ON divisions.division = matchs.Div
    GROUP BY country
    ORDER BY COUNT(*) DESC
    LIMIT 1;

12. **Which divisions have the most matches, and what is the number of matches per division?**
    ```sql
    SELECT country, division, COUNT(*) AS matchs_per_division
    FROM divisions
    LEFT JOIN matchs
    ON divisions.division = matchs.Div
    GROUP BY division
    ORDER BY COUNT(*) DESC;

13. **Which division has the most matches, and how many matches does it have?**
    ```sql
    SELECT country, division, COUNT(*) AS matchs_per_division
    FROM divisions
    LEFT JOIN matchs
    ON divisions.division = matchs.Div
    GROUP BY division
    ORDER BY COUNT(*) DESC
    LIMIT 1;

14. **What are the unique teams that have played as either home or away?**
    ```sql
    SELECT DISTINCT HomeTeam AS team
    FROM matchs
    UNION
    SELECT DISTINCT AWAYteam AS team
    FROM matchs;

15. **Which teams have played both as a home and away team?**
    ```sql
    SELECT DISTINCT HomeTeam AS team
    FROM matchs
    INTERSECT
    SELECT DISTINCT AWAYteam AS team
    FROM matchs;

16. **Which home teams have never played as away teams?**
    ```sql
    SELECT DISTINCT H.HomeTeam
    FROM matchs H
    LEFT JOIN matchs A
    ON H.HomeTeam = A.AwayTeam
    WHERE A.AWAYteam IS NULL;

17. **How many matches have the home team scored more goals than the away team?**
     ```sql
     SELECT COUNT(*) FROM matchs
     WHERE FTHG > FTAG;

18. **How many matches have the away team scored more goals than the home team?**
    ```sql
    SELECT COUNT(*) FROM matchs
    WHERE FTHG < FTAG;

19. **How many matches ended in a draw?**
    ```sql
    SELECT COUNT(*) FROM matchs
    WHERE FTHG = FTAG;

20. **What percentage of matches were won by the home team?**
    ```sql
    SELECT (COUNT(*) * 100) / (SELECT COUNT(*) FROM matchs)
    FROM matchs
    WHERE FTHG > FTAG;

21. **What is the winning percentage of each team, considering both home and away matches?**
    ```sql
    SELECT team, (SUM(win_by_team) * 100) /
    (SELECT COUNT(team)
    FROM (SELECT HomeTeam AS team FROM matchs
      UNION ALL
      SELECT AwayTeam AS team FROM matchs)
    GROUP BY team) AS percentage
    FROM (SELECT HomeTeam AS team, COUNT(HomeTeam) AS win_by_team
      FROM matchs
      WHERE FTR = "H"
      GROUP BY HomeTeam
      UNION
      SELECT AwayTeam, COUNT(AwayTeam)
      FROM matchs
      WHERE FTR = "A"
      GROUP BY AwayTeam)
   GROUP BY team
   ORDER BY percentage DESC;

22. **How many matches has each team played, including both home and away games?**
    ```sql
    SELECT team, COUNT(team)
    FROM (SELECT HomeTeam AS team FROM matchs
      UNION ALL
      SELECT AwayTeam AS team FROM matchs)
    GROUP BY team;

