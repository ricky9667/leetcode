---
title: 228. Summary Ranges
description:
date: 2024-12-02
tags: [Array]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun getRangeString(start: Int, end: Int) = if (start == end) "$start" else "$start->$end"

    fun summaryRanges(nums: IntArray): List<String> {
        if (nums.isEmpty()) return listOf()

        val result = mutableListOf<String>()
        var start = nums.first()

        for (i in 1 until nums.size) {
            if (nums[i] > nums[i-1] + 1) {
                val end = nums[i-1]
                result.add(getRangeString(start, end))
                start = nums[i]
            }
        }

        result.add(getRangeString(start, nums.last()))

        return result
    }
}
```
