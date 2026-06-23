# [Problem Name]

**Source:** [text](https://datalemur.com/questions/time-spent-snaps)
**Difficulty:** Easy / Medium / Hard
**Pattern(s):** e.g. window functions, recursive CTE, gaps-and-islands
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min (be honest — this is what you're tracking against interview timing)

## Problem

[1-2 line restatement in your own words — forces you to actually understand it]

## My Solution

```sql
SELECT
  age_bucket,
  ROUND((SUM(time_spent) FILTER(WHERE activity_type ='send')*100.0)/SUM(time_spent) FILTER(WHERE activity_type !='chat'), 2) AS send_perc,
  ROUND((SUM(time_spent) FILTER(WHERE activity_type ='open')*100.0)/SUM(time_spent) FILTER(WHERE activity_type !='chat'), 2) AS open_perc
FROM activities act
INNER JOIN age_breakdown ab ON ab.user_id = act.user_id
GROUP BY ab.age_bucket
```

## Why this approach

[1-3 sentences: why this pattern, what would break with a naive approach]

## What I'd say out loud in an interview

[Write the verbal explanation, not just the code. This is the part that closes your "verbal explanation under observation" gap — practice writing it, not just solving it.]

## Mistakes / what I got wrong first

[If you got it first try, skip. If not — this is the highest-value part of the file.]
