# [Problem Name]

**Source:** [text](https://datalemur.com/questions/user-retention)
**Difficulty:** Easy / Medium / Hard
**Pattern(s):** e.g. window functions, recursive CTE, gaps-and-islands
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min (be honest — this is what you're tracking against interview timing)

## Problem

[1-2 line restatement in your own words — forces you to actually understand it]

## My Solution

```sql
WITH mau AS (
  SELECT DISTINCT
    user_id,
    EXTRACT(MONTH FROM event_date) AS month
  FROM user_actions
  WHERE event_date >= '07/01/2022' AND event_date < '08/01/2022'
  AND user_id IN (
                    SELECT user_id
                    FROM user_actions
                    WHERE event_date >= '06/01/2022' AND event_date < '07/01/2022'
  )
)

SELECT
  month,
  COUNT(*) AS monthly_active_users
FROM mau
GROUP BY 1

-- SELECT
--   user_id, event_date
-- FROM user_actions
-- WHERE event_date >= '07/01/2022' AND event_date < '08/01/2022'
-- AND user_id IN (
--                   SELECT user_id
--                   FROM user_actions
--                   WHERE event_date >= '06/01/2022' AND event_date < '07/01/2022'
--                   )
```

## Why this approach

[1-3 sentences: why this pattern, what would break with a naive approach]

## What I'd say out loud in an interview

[Write the verbal explanation, not just the code. This is the part that closes your "verbal explanation under observation" gap — practice writing it, not just solving it.]

## Mistakes / what I got wrong first

[If you got it first try, skip. If not — this is the highest-value part of the file.]
