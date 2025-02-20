---
title: 452. Minimum Number of Arrows to Burst Balloons
description:
date: 2024-10-11
tags: [Array, Greedy, Sorting]
---

## Solution

先將 `points` 用 end 排序，每次選擇一個打擊點就選 last = point[1] 為射擊點，如果下一個 point 的 start <= last 就代表目前射擊點也可以打到下一個 point，接下來可以再看下一個有沒有符合這個條件。否則 start > last 的情況就打不到，那就更新 last = point[1] 並把射擊次數 +1。

### Implementation

```kotlin
class Solution {
    fun findMinArrowShots(points: Array<IntArray>): Int {
        val sortedPoints = points.sortedBy { it[1] }
        var shots = 1
        var last = sortedPoints[0][1]

        for (point in sortedPoints) {
            if (point[0] > last) {
                last = point[1]
                shots++
            }
        }

        return shots
    }
}
```
