---
title: 130. Surrounded Regions
description:
date: 2025-02-17
tags: [Array, Depth-First Search, Breadth-First Search, Union Find, Matrix]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun solve(board: Array<CharArray>): Unit {
        val m = board.size
        val n = board[0].size
        var region = mutableSetOf<Int>()

        fun encode(i: Int, j: Int): Int = i * n + j
        fun decode(index: Int): Pair<Int, Int> = (index / n) to (index % n)

        fun scan(i: Int, j: Int): Boolean {
            if (i < 0 || i >= m) return false
            if (j < 0 || j >= n) return false

            val index = encode(i, j)
            if (index in region) return true
            if (board[i][j] == 'X') return true
            
            region.add(index)
            return scan(i-1, j) && scan(i+1, j) && scan(i, j-1) && scan(i, j+1)
        }

        for (i in 0 until m) {
            for (j in 0 until n) {
                if (board[i][j] == 'X') continue

                val surround = scan(i, j)
                if (surround) {
                    region.forEach {
                        val (x, y) = decode(it)
                        board[x][y] = 'X'
                    }
                }
                region.clear()
            }
        }
    }
}
```
