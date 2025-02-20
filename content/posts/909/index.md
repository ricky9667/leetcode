---
title: 909. Snakes and Ladders
description:
date: 2025-02-15
tags: [Array, Breadth-First Search, Matrix]
---

## Solution

- 先把圖上面需要移動的點存到一個 Map 裡面，避免處理 index 的麻煩。
- 接下來再用 BFS 從 1 開始，每次把目前位置 +1 到 +6 的位置加到一個 Queue，如果 Map 裡面有 Key 代表需要移動，就改成移動後的位置加到 Queue，加到某個位置超過 n * n 就回傳 `count` 的結果。
- 如果是一定走不到終點的圖，會一直困在 BFS 的迴圈無法出來，因此用一個 Set `visited` 來看這格是否走過了，走過了就不再家回去 Queue。這樣走不到終點的圖會離開迴圈回傳 `-1`。

### Implementation

```kotlin
class Solution {
    fun snakesAndLadders(board: Array<IntArray>): Int {
        val n = board.size
        val map = mutableMapOf<Int, Int>()
        val visited = mutableSetOf<Int>()
        val q = LinkedList<Int>()

        for (i in 0 until n) {
            val isDesc = i % 2 == 1
            for (j in 0 until n) {
                val pos = if (isDesc) n - j - 1 else j
                val num = i * n + 1 + pos  
                val next = board[n-i-1][j]
                if (next != -1) map[num] = next
            }
        }

        q.add(1)
        var count = 0
        while (!q.isEmpty()) {
            count++
            var size = q.size
            while (size-- > 0) {
                val current = q.remove()
                for (p in 1..6) {
                    var next = current + p
                    if (next in visited) continue
                    visited.add(next)
                    next = map[current + p]?.let { it } ?: current + p
                    if (next >= n * n) return count
                    q.add(next)
                }
            }
        }

        return -1
    }
}
```
