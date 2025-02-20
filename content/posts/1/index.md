---
title: 1. Two Sum
description: 
date: 2024-10-13
tags: [Array, Hash Table]
---

## Solution

第一個迴圈先把每個數字以 number 當作 key、index 當作 value 加到一個 Map 裡面，第二個迴圈再直接用 target - 現在的數字當作 key 去找 Map 裡面有沒有這個 key value pair。
有找到值就回傳結果，-1 代表還沒找到，就繼續找到有為止。

### Implementation

```kotlin
class Solution {
    fun twoSum(nums: IntArray, target: Int): IntArray {
        val map = mutableMapOf<Int, Int>()

        for (i in 0 until nums.size) {
            map[nums[i]] = i
        }

        var result = intArrayOf()

        for (i in 0 until nums.size) {
            val find = target - nums[i]
            val index = map[find] ?: -1

            if (index == i) continue
            if (index != -1) {
                result = intArrayOf(i, index)
                break
            }
        }

        return result
    }
}
```
