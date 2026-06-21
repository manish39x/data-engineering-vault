# Employee Hierarchy — Transitive Closure (Example Entry)

**Source:** Practice (example — replace with your real solved problems)
**Difficulty:** Hard
**Pattern(s):** recursive CTE, hierarchy traversal, transitive closure
**Date solved:** 2026-06-21
**Time taken:** 14 min

## Problem
Given an `employees` table with `id` and `manager_id`, find every employee under a given manager at any depth (not just direct reports).

## My Solution
```sql
WITH RECURSIVE subordinates AS (
    SELECT id, manager_id, 1 AS depth
    FROM employees
    WHERE manager_id = :target_manager_id

    UNION ALL

    SELECT e.id, e.manager_id, s.depth + 1
    FROM employees e
    JOIN subordinates s ON e.manager_id = s.id
)
SELECT * FROM subordinates ORDER BY depth;
```

## Why this approach
A plain JOIN only gets one level deep. Recursive CTEs build the result iteratively: the anchor member finds direct reports, then the recursive member repeatedly joins the growing result against `employees` until no new rows are found (PostgreSQL stops automatically when a recursive step returns zero rows).

## What I'd say out loud in an interview
"This is a transitive closure problem — I need everyone reachable from the target manager through the manager_id relationship, not just direct reports. A recursive CTE has two parts: an anchor query that seeds the base case — direct reports — and a recursive query that joins the CTE back to itself, walking one level deeper each iteration. It terminates when a recursive step adds no new rows. I'm tracking depth here too since that's often asked as a follow-up — like 'who's exactly 2 levels down.'"

## Mistakes / what I got wrong first
First attempt forgot `UNION ALL` vs `UNION` — using `UNION` here silently dedupes and is slightly slower; `UNION ALL` is correct unless you specifically expect duplicate paths to a node (e.g. true graphs with multiple paths, not trees).
