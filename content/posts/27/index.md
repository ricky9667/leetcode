---
title: 27. Remove Element
description:
date: 2024-07-27
tags: [Array, Two Pointers]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun removeElement(nums: IntArray, `val`: Int): Int {
        val result = mutableListOf<Int>()
        
        // Add elements to `result` when != `val`
        for (i in 0 until nums.size) {
            if (nums[i] != `val`) {
                result.add(nums[i])
            }
        }

        // Copy back to `result`
        for (i in 0 until result.size) {
            nums[i] = result[i]
        }

        return result.size
    }
}
```
