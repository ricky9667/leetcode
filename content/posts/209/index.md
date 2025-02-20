---
title: 209. Minimum Size Subarray Sum
description:
date: 2024-10-29
tags: [Array, Binary Search, Sliding Window, Prefix Sum]
---

## Solution

- 開兩個 pointer `l`, `r`  分別指著 Sub Array 的兩端，如果 Sub Array 加起來的和 ≥ `target` 就讓 `l` 往右一格，否則 `r` 往右一格。
- 用上面方法的同時，Sub Array 的和 ≥ `target` 就計算 `l ~ r` 的距離，如果距離比目前最短距離小就換掉。

### Implementation

```kotlin
class Solution {
    fun minSubArrayLen(target: Int, nums: IntArray): Int {
        var result: Int? = null
        var currentSum = nums[0]
        var l = 0
        var r = 0

        while (l < nums.size || r < nums.size) {
            if (currentSum >= target) {
                val p = r - l + 1
                if (result == null || result > p) result = p
                currentSum -= nums[l++]
            } else {
                if (r == nums.lastIndex) break
                currentSum += nums[++r]
            }
        }

        return result ?: 0
    }
}
```
