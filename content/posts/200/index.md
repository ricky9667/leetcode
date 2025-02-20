---
title: 200. Number of Islands
description:
date: 2025-02-12
tags: [Array, Depth-First Search, Breadth-First Search, Union Find, Matrix]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun numIslands(grid: Array<CharArray>): Int {
        val m = grid.size
        val n = grid[0].size

        var islands = 0

        fun scan(i: Int, j: Int): Boolean {
            if (i !in 0..m-1) return false
            if (j !in 0..n-1) return false
            if (grid[i][j] == '0') return false

            grid[i][j] = '0'
            scan(i-1, j)
            scan(i+1, j)
            scan(i, j-1)
            scan(i, j+1)

            return true
        }

        for (i in 0 until m) {
            for (j in 0 until n) {
                if (scan(i, j)) islands++
            }
        }

        return islands
    }
}
```
