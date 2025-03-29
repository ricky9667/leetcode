---
title: 120. Triangle
description:
date: '2025-03-29T19:34:31+08:00'
tags: [Array, Dynamic Programming]
---

## Solution

- 在 `dp` 中存三角形第 `i` 層每個位置最小路徑和是多少， `i` 跑到下一層時再覆蓋掉上一層。每一次更新 dp 必須從 last index 倒過來算，index 0 需要是最後算的，不然會被覆蓋掉。
- Time: `O(n^2)`, Space: `O(n)`

### Implementation

```kotlin
class Solution {
    fun minimumTotal(triangle: List<List<Int>>): Int {
        val dp = IntArray(triangle.size)
        dp[0] = triangle[0][0]

        for (i in 1 until triangle.size) {
            var j = i
            dp[j] = triangle[i][j] + dp[j-1]
            while (--j > 0) {
                dp[j] = triangle[i][j] + min(dp[j-1], dp[j])
            }
            dp[0] = triangle[i][j] + dp[0]
        }

        return dp.min()
    }
}
```
