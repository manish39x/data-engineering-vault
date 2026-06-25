# [Problem Name]

**Source:** [text](https://datalemur.com/questions/matching-skills)
**Pattern(s):**
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min (be honest — this is what you're tracking against interview timing)

## Problem

[1-2 line restatement in your own words — forces you to actually understand it]

## My Solution

```sql
SELECT candidate_id
FROM (
  SELECT
    candidate_id,
    COUNT(*) FILTER(WHERE skill in ('Python', 'Tableau', 'PostgreSQL')) no_of_skill
  FROM candidates
  GROUP BY candidate_id
) c
WHERE no_of_skill = 3
ORDER BY candidate_id
```

## Why this approach

[1-3 sentences: why this pattern, what would break with a naive approach]

## What I'd say out loud in an interview

[Write the verbal explanation, not just the code. This is the part that closes your "verbal explanation under observation" gap — practice writing it, not just solving it.]

## Mistakes / what I got wrong first

[If you got it first try, skip. If not — this is the highest-value part of the file.]
