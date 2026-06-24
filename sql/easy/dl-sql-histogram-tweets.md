# [Problem Name]

**Source:** [text](https://datalemur.com/questions/sql-histogram-tweets)
**Pattern(s):**
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min (be honest — this is what you're tracking against interview timing)

## Problem

[1-2 line restatement in your own words — forces you to actually understand it]

## My Solution

```sql
WITH agg_tweet AS (
  SELECT
    user_id,
    COUNT(*) AS no_of_tweet
  FROM tweets
  WHERE tweet_date BETWEEN '2022-01-01 00:00:00' AND '2022-12-31 23:59:59'
  GROUP BY user_id
)

SELECT
  no_of_tweet AS tweet_bucker,
  COUNT(user_id) AS users_num
FROM agg_tweet
GROUP BY no_of_tweet
```

## Why this approach

[1-3 sentences: why this pattern, what would break with a naive approach]

## What I'd say out loud in an interview

[Write the verbal explanation, not just the code. This is the part that closes your "verbal explanation under observation" gap — practice writing it, not just solving it.]

## Mistakes / what I got wrong first

[If you got it first try, skip. If not — this is the highest-value part of the file.]
