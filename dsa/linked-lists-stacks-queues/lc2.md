# [Problem Name]

**Source:** [text](https://leetcode.com/problems/add-two-numbers/description/?envType=problem-list-v2&envId=plakya4j)
**Difficulty:** Easy / Medium / Hard
**Topic:** e.g. hashmaps, two-pointers
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min

## Problem

[1-2 line restatement in your own words]

## My Solution

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        carry = 0
        dummyHead = ListNode(0)
        tail = dummyHead
        while l1 is not None or l2 is not None or carry != 0:
            digit1 = l1.val if l1 is not None else 0
            digit2 = l2.val if l2 is not None else 0

            sum = digit1 + digit2 + carry
            digit = sum % 10
            carry = sum // 10

            newNode = ListNode(digit)
            tail.next = newNode
            tail = tail.next

            l1 = l1.next if l1 is not None else None
            l2 = l2.next if l2 is not None else None


        result = dummyHead.next
        dummyHead.next = None
        return result
```

## Complexity

- Time: O(?)
- Space: O(?)

## Why this approach

[The pattern recognition: what about this problem signaled "use a hashmap" or "use two pointers"]

## What I'd say out loud in an interview

[The verbal walkthrough — start with brute force, then explain the optimization]

## Mistakes / what I got wrong first
