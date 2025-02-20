---
title: 15. 3Sum
description:
date: 2024-10-21
tags: [Array, Two Pointers, Sorting]
---

## Solution

一開始需要先按照大小排序，接下來按照順序鎖定第一個數字 `sortedNums[i]` 後，剩下兩個數字加起來會等於 `-sortedNums[i]`，接下來可以利用 Two Sum 的作法去尋找剩下兩個值。

而這次可能會有多個解，並且我們需要排除掉重複解，所以三個 index `i`, `l`, `r` 在遇到一樣的數字的時候就要跳過，避免記錄到重覆解。這裡也可以用 Set 來自動處理。

### Implementation

```kotlin
class Solution {
    fun threeSum(nums: IntArray): List<List<Int>> {
        val result = mutableListOf<List<Int>>()
        val sortedNums = nums.sorted()

        for (i in 0 until sortedNums.size) {
            if (i > 0 && sortedNums[i] == sortedNums[i - 1]) continue

            val target = -sortedNums[i]
            var l = i + 1
            var r = sortedNums.lastIndex

            while (l < r) {
                val sum = sortedNums[l] + sortedNums[r]
                if (sum == target) {
                    result.add(listOf(sortedNums[i], sortedNums[l], sortedNums[r]))
                    while (l < r && sortedNums[l] == sortedNums[l + 1]) l++
                    while (l < r && sortedNums[r] == sortedNums[r - 1]) r--
                }
                if (sum > target) r-- else l++
            }
        }

        return result
    }
}
```
