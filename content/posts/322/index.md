---
title: 322. Coin Change
description:
date: '2025-03-24T15:58:39+08:00'
tags: [Array, Dynamic Programming, Breadth-First Search]
---

## Solution

背包問題

### Implementation

```kotlin
class Solution {
    fun coinChange(coins: IntArray, amount: Int): Int {
        val dp = IntArray(amount + 1) { -1 }
        dp[0] = 0
        
        for (value in 1..amount) {
            for (coin in coins) {
                val prev = value - coin
                if (prev < 0 || dp[prev] == -1) continue
                dp[value] = if (dp[value] == -1) dp[prev] + 1 else min(dp[value], dp[prev] + 1) 
            }
        }

        return dp[amount]
    }
}
```
