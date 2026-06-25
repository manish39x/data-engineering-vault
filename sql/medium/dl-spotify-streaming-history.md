# [Problem Name]

**Source:** [text](https://datalemur.com/questions/spotify-streaming-history)
**Pattern(s):**
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min (be honest — this is what you're tracking against interview timing)

## Problem

[1-2 line restatement in your own words — forces you to actually understand it]

## My Solution

```sql
WITH merged_data AS (
  SELECT user_id, song_id, song_plays FROM songs_history
  UNION ALL
  SELECT
    user_id,
    song_id,
    COUNT(*) AS song_plays
  FROM songs_weekly WHERE listen_time < '2022-08-04 23:59:59'
  GROUP BY user_id, song_id
)

SELECT
  user_id, song_id,
  SUM(song_plays) AS song_plays
FROM merged_data
GROUP BY user_id, song_id
ORDER BY song_plays DESC
```

## Why this approach

[1-3 sentences: why this pattern, what would break with a naive approach]

## What I'd say out loud in an interview

[Write the verbal explanation, not just the code. This is the part that closes your "verbal explanation under observation" gap — practice writing it, not just solving it.]

## Mistakes / what I got wrong first

[If you got it first try, skip. If not — this is the highest-value part of the file.]
