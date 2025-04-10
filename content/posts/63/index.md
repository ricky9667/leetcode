---
title: 63. Unique Paths II
description:
date: '2025-04-10T10:34:19+08:00'
tags: [Array, Dynamic Programming, Matrix]
---

## Solution

`dp[i][j]` 代表 `index = (i, j)` 的路徑數，路徑數會是上面的跟左邊的路徑數和，如果遇到障礙物或牆壁則路徑數為 `0`。

Time: `O(MN)`, Space: `O(MN)`

### Implementation

```kotlin
class Solution {
    fun uniquePathsWithObstacles(obstacleGrid: Array<IntArray>): Int {
        val dp = obstacleGrid.copyOf()
        val (m, n) = dp.size to dp[0].size

        for (i in 0 until m) {
            for (j in 0 until n) {
                dp[i][j] = when {
                    obstacleGrid[i][j] == 1 -> 0
                    i + j == 0 -> 1
                    else -> {
                        val top = if (i != 0) dp[i-1][j] else 0
                        val left = if (j != 0) dp[i][j-1] else 0
                        top + left
                    }
                }
            }
        }

        return dp[m - 1][n - 1]
    }
}
```
