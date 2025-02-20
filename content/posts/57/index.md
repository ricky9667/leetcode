---
title: 57. Insert Interval
description:
date: 2024-12-09
tags: [Array]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun insert(intervals: Array<IntArray>, newInterval: IntArray): Array<IntArray> {
        val updatedIntervals = mutableListOf<IntArray>()
        val size = intervals.size
        var i = 0

        while (i < size && intervals[i][1] < newInterval[0]) {
            updatedIntervals.add(intervals[i++])
        }

        while (i < size && newInterval[0] <= intervals[i][1] && newInterval[1] >= intervals[i][0]) {
            newInterval[0] = min(newInterval[0], intervals[i][0])
            newInterval[1] = max(newInterval[1], intervals[i][1])
            i++
        }

        updatedIntervals.add(newInterval)

        while (i < size) {
            updatedIntervals.add(intervals[i++])
        }

        return updatedIntervals.toTypedArray()
    }
}
```