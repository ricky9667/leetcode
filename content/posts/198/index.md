---
title: 198. House Robber
description:
date: '2025-03-21T10:34:05+08:00'
tags: [Array, Dynamic Programming]
---

## Solution

Time: `O(n)`, Space: `O(n)`

### Implementation

```kotlin
class Solution {
    fun rob(nums: IntArray): Int {
        if (nums.size == 1) return nums[0]
        
        val dp = IntArray(nums.size)
        dp[0] = nums[0]
        dp[1] = max(nums[0], nums[1])

        for (i in 2 until nums.size) {
            dp[i] = max(dp[i-1], dp[i-2] + nums[i])
        }

        return dp.last()
    }
}
```
