---
title: 11. Container With Most Water
description: 
date: 2024-10-22
tags: [Array, Two Pointers, Greedy]
---

## Solution

- Leetcode 上面的 Hint 2 就差不多把題目的大綱講出來了，主要方法是盡可能找到最高的兩個水柱，然後這兩個水柱越長越好，這樣才能包到的面積是最大的。
- 做法是從水柱兩側開始尋找，讓 `l` 和 `r` 兩個 index 從兩側往內移動，這樣就能優先選到比較遠的兩個水柱算 `maxArea`。
- 另外，因為我們還需要盡可能找最高的水柱，所以我們會選 `height[l]` 和 `height[r]` 中比較矮的水柱，這樣就能在我們每次算 `maxArea` 時都選到比較高的水柱。
- 最後回傳 `maxArea` 就是解答了。

### Implementation

```kotlin
class Solution {
    fun maxArea(height: IntArray): Int {
        var maxArea = 0
        var l = 0
        var r = height.lastIndex

        while (l < r) {
            val currentArea = (r - l) * min(height[l], height[r])
            maxArea = max(maxArea, currentArea)
            if (height[l] < height[r]) l++ else r--
        }

        return maxArea
    }
}
```
