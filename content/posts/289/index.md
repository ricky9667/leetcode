---
title: 289. Game of Life
description:
date: 2024-11-26
tags: [Array, Matrix, Simulation]
---

## Solution 1

- 建立一個二維 Array `neighbors` 紀錄每一格旁邊有幾個 1 的格子，紀錄好之後再跑一次迴圈用 `neighbors` 和舊的 `board` 計算每一格是否活著。
- 空間複雜度是 `O(n^2)` 。

### Implementation

```kotlin
class Solution {
    fun gameOfLife(board: Array<IntArray>): Unit {
        val height = board.size
        val width = board[0].size
        val neighbors = Array(height) { Array<Int>(width) { 0 } }

        for (i in 0 until height) {
            for (j in 0 until width) {
                for (ni in (i-1)..(i+1)) {
                    if (ni < 0 || ni >= height) continue
                    for (nj in (j-1)..(j+1)) {
                        if (nj < 0 || nj >= width) continue
                        if (ni == i && nj == j) continue
                        neighbors[i][j] += board[ni][nj]
                    }
                }
            }
        }

        for (i in 0 until height) {
            for (j in 0 until width) {
                val live = neighbors[i][j] == 3 || (neighbors[i][j] == 2 && board[i][j] == 1)
                board[i][j] = if (live) 1 else 0
            }
        }
    }
}
```

## Solution 2

- 因為發現鄰居最多只會有 8， `board` 和 `neighbors` 中的數字不會超過 10 的情況下，可以偷吃步把 `neighbors` 紀錄在 `board` 的十位數，就能在不建立新的空間的情況下紀錄鄰居。
- 空間複雜度縮減為 `O(1)`。

### Implementation

```kotlin
class Solution {
    fun gameOfLife(board: Array<IntArray>): Unit {
        val height = board.size
        val width = board[0].size

        for (i in 0 until height) {
            for (j in 0 until width) {
                var neighbors = 0
                for (ni in (i-1)..(i+1)) {
                    if (ni < 0 || ni >= height) continue
                    for (nj in (j-1)..(j+1)) {
                        if (nj < 0 || nj >= width) continue
                        if (ni == i && nj == j) continue
                        neighbors += board[ni][nj] % 10
                    }
                }
                board[i][j] += neighbors * 10
            }
        }

        for (i in 0 until height) {
            for (j in 0 until width) {
                val live = board[i][j] / 10 == 3 || (board[i][j] / 10 == 2 && board[i][j] % 10 == 1)
                board[i][j] = if (live) 1 else 0
            }
        }
    }
}
```
