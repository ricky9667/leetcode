---
title: 26. Remove Duplicates from Sorted Array
description:
date: 2024-07-27
tags: [Array, Two Pointers]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun removeDuplicates(nums: IntArray): Int {
        val result = mutableListOf<Int>()

        for (i in 0 until nums.size) {
            if (i == 0 || nums[i] > result.last()) {
                result.add(nums[i])
            }
        }

        for (i in 0 until result.size) {
            nums[i] = result[i]
        }

        return result.size
    }
}
```
