---
title: 53. Maximum Subarray
description: 
date: '2025-03-12T14:20:45+08:00'
tags: [Array, Divide and Conquer, Dynamic Programming]
---

## Solution 1

Dynamic Programming

### Implementation

```kotlin
class Solution {
    fun maxSubArray(nums: IntArray): Int {
        val dp = IntArray(nums.size)
        var result = nums[0]
        dp[0] = nums[0]

        for (i in 1 until nums.size) {
            dp[i] = max(dp[i-1] + nums[i], nums[i])
            result = max(dp[i], result)
        }
        return result
    }
}
```

## Solution 2

Divide and Conquer

### Implementation

```kotlin
class Solution {
    fun maxSubArray(nums: IntArray): Int {
        if (nums.size == 1) return nums[0]

        val m = nums.size / 2
        val leftMax = maxSubArray(nums.copyOfRange(0, m))
        val rightMax = maxSubArray(nums.copyOfRange(m, nums.size))

        var s = 0
        var maxSum = nums[m]
        for (i in m downTo 0) {
            s += nums[i]
            maxSum = max(maxSum, s)
        }

        s = maxSum
        for (i in m + 1 until nums.size) {
            s += nums[i]
            maxSum = max(maxSum, s)
        }

        return maxOf(leftMax, rightMax, maxSum)
    }
}
```
