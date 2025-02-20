---
title: 88. Merge Sorted Array
description:
date: 2024-07-26
tags: [Array, Two Pointers, Sorting]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun merge(nums1: IntArray, m: Int, nums2: IntArray, n: Int): Unit {
        var pm = 0
        var pn = 0

        val size = m + n
        val result = nums1.copyOf()

        while (pm + pn < size) {
            if (pn >= n) {
                result[pm + pn] = nums1[pm++]
                continue
            }

            if (pm >= m) {
                result[pm + pn] = nums2[pn++]
                continue
            }
            
            if (nums1[pm] > nums2[pn]) {
                result[pm + pn] = nums2[pn++]
            } else {
                result[pm + pn] = nums1[pm++]
            }
        }

        for (i in 0 until size) {
            nums1.set(i, result[i])
        }
    }
}
```
