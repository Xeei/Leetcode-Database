## Question
https://leetcode.com/problems/game-play-analysis-iv/description/

### Answer
```sql
with first_login as (
    SELECT *, DENSE_RANK() OVER(PARTITION BY player_id ORDER BY event_date asc) as rank
    FROM Activity
)

SELECT 
ROUND(
    CAST(COUNT(*) as numeric)
    /
    CAST((
        SELECT COUNT(*) 
        FROM (
            SELECT DISTINCT player_id FROM Activity
        )
    ) as numeric)
    , 2) 
as fraction
FROM first_login t1

INNER JOIN Activity t2
ON t2.player_id = t1.player_id
AND t2.event_date - 1 = t1.event_date
AND t1.rank = 1
```
