---
title: 300. Longest Increasing Subsequence
description:
date: '2025-05-22T13:12:53+08:00'
tags: [Array, Binary Search, Dynamic Programming]
---

## Solution

- 參考 [Longest Increasing Subsequence - Neetcode](https://youtu.be/cjWnW0hdF1Y?si=OdGQz1rEHSzo5ui5)
- 用 dp[i] 陣列紀錄 i 到 n-1 的 LIS 是多少，每次把 i + 1 ~ n-1 跑過一遍看把 nums[i] 算進去之後的 LIS 誰最大，跑完之後再把 i— 後再重新做一樣的事。最後 dp 裡面最大的數字就是解答。
- Time: O(n^2), Space: O(n)

### Implementation

```kotlin
class Solution {
    fun lengthOfLIS(nums: IntArray): Int {
        val dp = IntArray(nums.size) { 1 }
        var i = nums.size

        while (--i >= 0) {
            for (j in i + 1 until nums.size) {
                if (nums[j] > nums[i]) dp[i] = max(dp[i], 1 + dp[j])
            }
        }

        return dp.max()
    }
}
```
