# [Problem Name]

**Source:** [text](https://leetcode.com/problems/longest-palindromic-substring/description/)
**Difficulty:** Easy / Medium / Hard
**Topic:** e.g. hashmaps, two-pointers
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min

## Problem

[1-2 line restatement in your own words]

## My Solution

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        s_prime = "#" + "#".join(s) + "#"
        radii = [0 for _ in range(len(s_prime))] # length of palindrome from center to one end
        center = 0
        right_border = 0
        max_radius = 0
        largest_palindrome_center = 0
        for i in range(len(s_prime)):
            mirror = center - (i - center) # index of mirror letter

            #if the current letter exists within a larger palindrome
            if i < right_border:
                # if the mirror palindrome dosnt extend largest palindrome just copy
                if radii[mirror] < right_border - i:
                    radii[i] = radii[mirror]
                    continue
                # if the mirror palindrome extends beyond or upto the border of the largest palindrom centerd at 'center' then we know that
                else:
                    radii[i] = right_border - i

            # now we need to explore beyond the minimum guaranteed length defined in line 20
            # if `s_prime[i] is NOT within a larger palindrome, then radii[i] would be 0 and we'd be exploring from scratch`
            while i - 1 - radii[i] >= 0 \
                and i + 1 + radii[i] < len(s_prime) \
                and s_prime[i-1-radii[i]] == s_prime[i+1+radii[i]]:

                radii[i] += 1

            # if the palindrome centered at `i` extends beyond the palindrome centered
            # at `center`
            if i + radii[i] > right_border:
                # reset center and right_border to `i` and `i+radii[i]` because the
                # current palindrome is the palindrome that reaches the furthest to the right
                center = i
                right_border = i + radii[i]

            if radii[i] > max_radius:
                max_radius = radii[i]
                largest_palindrome_center = i

        # max_radius is a "radius" in s_prime but the full length of the palindrome in `s`
        start_index = (largest_palindrome_center - max_radius) // 2
        return s[start_index : start_index + max_radius]

```

## Complexity

- Time: O(?)
- Space: O(?)

## Why this approach

[The pattern recognition: what about this problem signaled "use a hashmap" or "use two pointers"]

## What I'd say out loud in an interview

[The verbal walkthrough — start with brute force, then explain the optimization]

## Mistakes / what I got wrong first
