# [Problem Name]

**Source:** https://datalemur.com/questions/sql-top-three-salaries
**Pattern(s):**
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min (be honest — this is what you're tracking against interview timing)

## Problem

[1-2 line restatement in your own words — forces you to actually understand it]

## My Solution

```sql
-- WITH top_three_salary_range AS (
--   SELECT DISTINCT department_id, salary
--   FROM (
--     SELECT
--       department_id,
--       salary,
--       DENSE_RANK() OVER(PARTITION BY department_id ORDER BY salary DESC) AS rn
--     FROM employee
--   ) AS te
--   WHERE rn = 3
-- ), obt AS (
--   SELECT
--     d.department_name, e.name, e.salary
--   FROM employee e
--   INNER JOIN department d ON e.department_id = d.department_id
--   INNER JOIN top_three_salary_range ts ON ts.department_id = e.department_id
--   WHERE e.salary >= ts.salary
--   ORDER BY d.department_name ASC, e.salary DESC, e.name ASC
-- )
-- SELECT * FROM obt


WITH ranked_employees AS (
  SELECT
    d.department_name,
    e.name,
    e.salary,
    DENSE_RANK() OVER(PARTITION BY e.department_id ORDER BY e.salary DESC) AS rn
  FROM employee e
  INNER JOIN department d ON e.department_id = d.department_id
)
SELECT department_name, name, salary
FROM ranked_employees
WHERE rn <= 3
ORDER BY department_name ASC, salary DESC, name ASC;
```

## Why this approach

[1-3 sentences: why this pattern, what would break with a naive approach]

## What I'd say out loud in an interview

[Write the verbal explanation, not just the code. This is the part that closes your "verbal explanation under observation" gap — practice writing it, not just solving it.]

## Mistakes / what I got wrong first

[If you got it first try, skip. If not — this is the highest-value part of the file.]
