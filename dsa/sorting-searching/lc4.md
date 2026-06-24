# [Problem Name]

**Source:** [text](https://leetcode.com/problems/median-of-two-sorted-arrays/)
**Difficulty:** Easy / Medium / Hard
**Topic:** e.g. hashmaps, two-pointers
**Date solved:** YYYY-MM-DD
**Time taken:** \_ min

## Problem

[1-2 line restatement in your own words]

## My Solution

```cpp
#include <bits/stdc++.h>

class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int n1 = nums1.size();
        int n2 = nums2.size();
        if(n1 > n2) return findMedianSortedArrays(nums2, nums1); // make sure n1 is shortest one
        int partition = (n1+n2+1)/2;
        int low = 0, high = n1;
        while (low <= high){
            int mid1 = (low+high)/2;
            int mid2 = partition - mid1;

            int l1 = INT_MIN, l2 = INT_MIN;
            int r1 = INT_MAX, r2 = INT_MAX;

            if(mid1 < n1) r1 = nums1[mid1];
            if(mid2 < n2) r2 = nums2[mid2];
            if(mid1-1 >= 0) l1 = nums1[mid1-1];
            if(mid2-1 >= 0) l2 = nums2[mid2-1];

            if(l1 > r2) high = mid1-1;
            else if(l2 > r1) low = mid1+1;
            else {
                if((n1+n2)%2 == 0) return (max(l1, l2)+min(r1,r2))/2.0;
                else return double(max(l1, l2));
            }
        }
        return double(1);
    }
};
```

## Complexity

- Time: O(?)
- Space: O(?)

## Why this approach

[The pattern recognition: what about this problem signaled "use a hashmap" or "use two pointers"]

## What I'd say out loud in an interview

[The verbal walkthrough — start with brute force, then explain the optimization]

## Mistakes / what I got wrong first
