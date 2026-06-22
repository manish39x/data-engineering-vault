# [Problem Name]

**Source:** [text](https://datalemur.com/questions/sql-third-transaction)
**Difficulty:** Easy / Medium / Hard
**Pattern(s):** e.g. window functions, recursive CTE, gaps-and-islands
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min (be honest — this is what you're tracking against interview timing)

## Problem

[1-2 line restatement in your own words — forces you to actually understand it]

## My Solution

```sql
WITH ranked_transaction AS (
  SELECT
    *,
    ROW_NUMBER() OVER(PARTITION BY user_id ORDER BY transaction_date) AS rn
  FROM transactions
)

SELECT
  user_id, spend, transaction_date
FROM ranked_transaction
WHERE rn = 3
```

## Why this approach

[1-3 sentences: why this pattern, what would break with a naive approach]

## What I'd say out loud in an interview

[Write the verbal explanation, not just the code. This is the part that closes your "verbal explanation under observation" gap — practice writing it, not just solving it.]

## Mistakes / what I got wrong first

[If you got it first try, skip. If not — this is the highest-value part of the file.]
