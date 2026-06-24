# [Problem Name]

**Source:** [text](https://datalemur.com/questions/sql-highest-grossing)
**Pattern(s):**
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min (be honest — this is what you're tracking against interview timing)

## Problem

[1-2 line restatement in your own words — forces you to actually understand it]

## My Solution

```sql
WITH aggregated_product AS(
  SELECT
    category, product,
    SUM(spend) AS total_spend
  FROM product_spend
  WHERE transaction_date BETWEEN '2022-01-01 00:00:00' AND '2022-12-31 23:59:59'
  GROUP BY category, product
), ranked AS (
  SELECT
    category, product,
    total_spend,
    ROW_NUMBER() OVER(PARTITION BY category ORDER BY total_spend DESC) as rn
  FROM aggregated_product
)

SELECT
  category, product,
  total_spend
FROM ranked
WHERE rn < 3
```

## Why this approach

[1-3 sentences: why this pattern, what would break with a naive approach]

## What I'd say out loud in an interview

[Write the verbal explanation, not just the code. This is the part that closes your "verbal explanation under observation" gap — practice writing it, not just solving it.]

## Mistakes / what I got wrong first

[If you got it first try, skip. If not — this is the highest-value part of the file.]
