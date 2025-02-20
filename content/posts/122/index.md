---
title: 122. Best Time to Buy and Sell Stock II
description:
date: 2024-08-04
tags: [Array, Dynamic Programming, Greedy]
---

## Solution 1

使用貪婪演算法 (Greedy)，在迭代整個 Array 過程中，

1. 如果數字 `prices[i]` 小於 `prices[i-1]` ，更新 `lowestPrice`。
2. 如果數字 `prices[i]` 大於 `prices[i-1]` ，將目前和 `lowestPrice` 的差加進 `maxProfit`，並更新 `lowestPrice`。

### Example 1-1

| `i` | `prices[i]` | `lowestPrice` | `maxProfit` |
| --- | ----------- | ------------- | ----------- |
|   0 |           7 |             7 |           0 |
|   1 |           1 |             1 |           0 |
|   2 |           5 |             5 | 0 + (5 - 1) = 4 |
|   3 |           3 |             3 |           4 |
|   4 |           6 |             6 | 4 + (6 - 3) = 7 |
|   5 |           4 |             4 |           7 |

### Implementation

```kotlin
class Solution {
    fun maxProfit(prices: IntArray): Int {
        var lowestPrice = prices[0]
        var currentMaxProfit = 0

        for (i in 0 until prices.size) {
            if (prices[i] < lowestPrice) {
                lowestPrice = prices[i]
            } else if (prices[i] > lowestPrice) {
                currentMaxProfit += prices[i] - lowestPrice
                lowestPrice = prices[i]
            }
        }

        return currentMaxProfit
    }
}
```

## Solution 2

以上的 Greedy 可以進行常數優化。

先將 `prices` 進行差分運算，計算出相鄰兩個數字 `prices[i]` 和 `prices[i-1]` 相減後，將相差 > 0 的值相加即為解答。

### Example 2-1

- 輸入：`[7, 1, 5, 3, 6, 4]`
- 進行差分計算：`[-6, 4, -2, 3, -2]`
- 把數值為正相加：`4 + 3 = 7`

### Implementation

```kotlin
class Solution {
    fun maxProfit(prices: IntArray): Int {
        var maxProfit = 0
        for (i in 1 until prices.size) {
            maxProfit += max(prices[i] - prices[i-1], 0)
        }
        return maxProfit
    }
}
```