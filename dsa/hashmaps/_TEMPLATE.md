# [Problem Name]

**Source:** LeetCode
**Difficulty:** Easy
**Topic:** hashmaps
**Date solved:** 2026-06-21
**Time taken:** \_ 5

## Problem

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

### Example\*\* 1:

**Input**: nums = [2,7,11,15], target = 9
**Output**: [0,1]
**Explanation**: Because nums[0] + nums[1] == 9, we return [0, 1].

## My Solution

```python
class Solution:
  def twoSum(self, nums: List[int], target: int) -> List[int]:
    seen = {}
    for index, num in enumerate(nums):
      remaining = target - num
      if remaining in seen:
        return [seen[remaining], index]

      seen[num] = index
```

## Complexity

- Time: O(n)
- Space: O(n)

## Why this approach

because its easy and fast to implement and time complexity is O(n)
yah we also have two pointer but to use that your data must be sorted that will take same time complexity but O(1) space complexity

## What I'd say out loud in an interview

[The verbal walkthrough — start with brute force, then explain the optimization]

## Mistakes / what I got wrong first
