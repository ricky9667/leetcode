---
title: 51. N-Queens
description:
date: '2025-05-10T12:25:35+08:00'
tags: [Array, Backtracking]
---

## Solution

Backtracking 的時候每次都先把後面沒辦法放的位置都標 `x` ，再下一層的位置如果是 `x` 就直接跳過。

### Code

```kotlin
class Solution {
    fun solveNQueens(n: Int): List<List<String>> {
        val result = mutableListOf<List<String>>()
        val emptyBoard = MutableList(n) { CharArray(n) { '.' } }

        fun solve(i: Int, board: MutableList<CharArray>) {
            if (i == n) {
                board.forEach { row ->
                    for (index in row.indices) {
                        if (row[index] == 'x') row[index] = '.'
                    }
                }
                result.add(board.map { it.joinToString("") })
                return
            }

            for (j in 0 until n) {
                val current = board.map { it.copyOf() }.toMutableList()
                
                if (current[i][j] == 'x') continue
                current[i][j] = 'Q'

                var p = 0
                while (++p + i < n) {
                    current[i + p][j] = 'x'
                    if (j + p < n) current[i + p][j + p] = 'x'
                    if (j - p >= 0) current[i + p][j - p] = 'x'
                }
                
                solve(i + 1, current)
            }
        }

        solve(0, emptyBoard)
        return result
    }
}
```
