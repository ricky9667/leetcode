---
title: 121. Best Time to Buy and Sell Stock
description:
date: 2024-07-29
tags: [Array, Dynamic Programming]
---

## Solution

## Implementation

```kotlin
class Solution {
    fun maxProfit(prices: IntArray): Int {
        var lowestPrice = prices[0]
        var currentMaxProfit = 0

        prices.forEach { price ->
            if (price < lowestPrice) {
                lowestPrice = price
            }
            if (price - lowestPrice > currentMaxProfit) {
                currentMaxProfit = price - lowestPrice
            }
        }

        return currentMaxProfit
    }
}
```
