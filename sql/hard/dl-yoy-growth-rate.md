# [Problem Name]

**Source:** [text](https://datalemur.com/questions/yoy-growth-rate)
**Pattern(s):**
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min (be honest — this is what you're tracking against interview timing)

## Problem

[1-2 line restatement in your own words — forces you to actually understand it]

## My Solution

```sql
WITH Aggregate_transactions AS (
  SELECT
    EXTRACT(YEAR FROM transaction_date) AS year,
    product_id,
    SUM(spend) AS curr_year_spend
  FROM user_transactions
  GROUP BY 1, 2
)

SELECT
  year,
  product_id,
  curr_year_spend,
  LAG(curr_year_spend, 1) OVER(PARTITION BY product_id ORDER BY year) AS prev_year_spend,
  ROUND((
          (curr_year_spend/
          LAG(curr_year_spend,1) OVER(PARTITION BY product_id ORDER BY year))-1)*100.0, 2) AS yoy_rate
FROM Aggregate_transactions

```

## Why this approach

[1-3 sentences: why this pattern, what would break with a naive approach]

## What I'd say out loud in an interview

[Write the verbal explanation, not just the code. This is the part that closes your "verbal explanation under observation" gap — practice writing it, not just solving it.]

## Mistakes / what I got wrong first

[If you got it first try, skip. If not — this is the highest-value part of the file.]
