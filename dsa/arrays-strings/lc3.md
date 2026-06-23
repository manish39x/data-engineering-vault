# [Problem Name]

**Source:** [text](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)
**Difficulty:** Easy / Medium / Hard
**Topic:** e.g. hashmaps, two-pointers
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min

## Problem

[1-2 line restatement in your own words]

## My Solution

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        left = max_len = 0
        char_set = set()
        for right in range(len(s)):
            while s[right] in char_set:
                char_set.remove(s[left])
                left += 1

            char_set.add(s[right])
            max_len = max(max_len, right-left+1)

        return max_len
```

## Complexity

- Time: O(?)
- Space: O(?)

## Why this approach

[The pattern recognition: what about this problem signaled "use a hashmap" or "use two pointers"]

## What I'd say out loud in an interview

[The verbal walkthrough — start with brute force, then explain the optimization]

## Mistakes / what I got wrong first
