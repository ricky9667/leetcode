---
title: 134. Gas Station
description:
date: '2025-04-29T18:05:36+08:00'
tags: [Array, Greedy]
---

## Solution

- 第一個迴圈先把 `remain` 算出來，`remain` 裡面記得是從 i 開車到 i + 1 站會多或少的油量。在這個同時把全部的 `remain` 值加起來到 `tank`，如果總和 < 0 代表總共的油量不夠開一圈並且可以 early return。
- 接下來就倒過來加 `remain` 的總和加到 `tank`，並找出 `tank` 最高油量的時機，因為可以確定一定有答案，因此 tank 最高的 `index` 就是解答。
- Time: O(2n), Space: O(1)

### Implementation

```kotlin
class Solution {
    fun canCompleteCircuit(gas: IntArray, cost: IntArray): Int {
        fun remain(i: Int) = gas[i] - cost[i]

        var tank = 0
        for (i in 0 until gas.size) tank += remain(i)
        if (tank < 0) return -1

        tank = 0
        var startIndex = gas.lastIndex
        var maxTank = remain(startIndex)

        for (i in startIndex downTo 0) {
            tank += remain(i)
            if (tank > maxTank) {
                startIndex = i
                maxTank = tank
            }
        }

        return startIndex
    }
}
```
