## Question
https://leetcode.com/problems/human-traffic-of-stadium/description/

## Answer
[Submission](https://leetcode.com/problems/human-traffic-of-stadium/submissions/1868196282/)
```sql
with grps as (
    SELECT *,
    id - row_number() OVER(order by id) grp
    FROM Stadium    
    WHERE people >= 100
)

SELECT id, visit_date, people
FROM grps
WHERE grp IN (
    SELECT grp
    FROM grps
    GROUP BY grp
    HAVING COUNT(*) >= 3
)
```
