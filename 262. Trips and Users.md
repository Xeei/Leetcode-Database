## Question
https://leetcode.com/problems/trips-and-users/description/

## Answer
```sql
SELECT request_at as Day, 
ROUND(
    SUM(
        CASE WHEN t.status = 'completed' THEN 0
        ELSE 1
        END
    )::numeric / COUNT(*)
    , 2
) as "Cancellation Rate"

FROM Trips t

JOIN Users uc
ON uc.users_id = t.client_id

JOIN Users ud
ON ud.users_id = t.driver_id

WHERE request_at >= '2013-10-01' 
AND request_at < '2013-10-04'
AND uc.banned = 'No'
AND ud.banned = 'No'

GROUP BY request_at
```
