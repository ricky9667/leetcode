---
title: 128. Longest Consecutive Sequence
description:
date: 2024-11-27
tags: [Array, Hash Table, Union Find]
---

## Solution

- 想法是先建立一個 Map，Map 紀錄每個數字跟誰是同一個群組。每次遇到一個數字 `num`，就看 `num + 1` 和 `num - 1` 有沒有在 Map 裡面，有的話就把他們放在同一個群組，沒有的話就自成一群。
- 這個時候需要使用**並查集 (Disjoint Set)** 來記錄每一個群組，在每一次尋找群組的老大的時候，也會同時用遞迴更新群組的老大是誰。
- 最後再計算 哪一個老大出現最多次，所以算`boss` 裡面哪個 Value 出現最多次就是答案，

Reference: https://hackmd.io/@CLKO/rkRVS_o-4?type=view

### Implementation

```kotlin
class Solution {
    val boss = mutableMapOf<Int, Int>()

    fun findBoss(x: Int): Int {
        if (x == boss[x]) return x
        val currentBoss = findBoss(boss[x]!!)
        boss[x] = currentBoss
        return currentBoss
    }

    fun join(x: Int, y: Int) {
        val xBoss = findBoss(x)
        val yBoss = findBoss(y)
        boss[xBoss] = yBoss
    }

    fun longestConsecutive(nums: IntArray): Int {
        for (num in nums) {
            if (boss.containsKey(num)) continue
            boss[num] = num
            if (boss.containsKey(num - 1)) join(num - 1, num)
            if (boss.containsKey(num + 1)) join(num + 1, num)
        }

        val count = mutableMapOf<Int, Int>()

        for (num in boss.keys) {
            val currentBoss = findBoss(num)
            count[currentBoss] = count[currentBoss]?.let { it + 1 } ?: 1 
        }

        var ans = 0
        count.values.forEach { ans = max(ans, it) }

        return ans
    }
}
```
