---
title: 221. Maximal Square
description:
date: '2025-04-25T12:54:59+08:00'
tags: [Array, Dynamic Programming, Matrix]
---

## Solution

- 參考：[Maximum Square - Neetcode](https://youtu.be/6X7Ha2PrDmM?si=715GorMwc4hkmPkv)
- 先定義 dp 為「**在 (i, j) 這個坐標為右下角時，可以框出的最大正方形邊長**」，並透過這個方式把 dp 這個 Array 裡面的資料建立起來。
  - 如果 matrix[i][j] 是 0，那目前這格的 dp 值就是 0。
  - 如果 matrix[i][j] 是 1，而且目前的 (i, j) 在最靠左或靠上，那他最大能框出來的正方形就是 1。
  - 排除上面的情況，在定 (i, j) 可以框出多大的正方形時，我們會根據左邊、上面、左上方三個位置，這三個值的最小值 + 1 就是解答。
- 最後我們再把 dp 的每個位置跑過一遍，裡面的最大值平方後就是解答了。
- Time: O(MN), Space: O(MN)

### Implementation

```kotlin
class Solution {
    fun maximalSquare(matrix: Array<CharArray>): Int {
        val rows = matrix.size
        val cols = matrix[0].size
        val dp = Array(rows) { IntArray(cols) { -1 } }

        for (i in 0 until rows) {
            for (j in 0 until cols) {
                if (matrix[i][j] == '0') dp[i][j] = 0
                else if (i == 0 || j == 0) dp[i][j] = 1
                else {
                    val diag = dp[i-1][j-1]
                    val left = dp[i][j-1]
                    val top = dp[i-1][j]
                    dp[i][j] = 1 + minOf(diag, left, top)
                }
            }
        }
    
        var result = 0
        for (i in 0 until rows) {
            for (j in 0 until cols) {
                result = max(result, dp[i][j])
            }
        }

        return result * result
    }
}
```
