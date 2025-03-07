---
title: 35. Search Insert Position
description:
date: '2025-03-07T17:11:03+08:00'
tags: [Array, Binary Search]
---

### Implementation

```kotlin
class Solution {
    fun searchInsert(nums: IntArray, target: Int): Int {
        var (l, r) = 0 to nums.size
        var m = nums.size / 2

        while (r - l > 1) {
            if (nums[m] == target) return m
            if (nums[m] > target) r = m else l = m
            m = (l + r) / 2
        }

        return if (target <= nums[l]) l else r
    }
}
```
