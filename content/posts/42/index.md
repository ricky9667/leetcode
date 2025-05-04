---
title: 42. Trapping Rain Water
description:
date: '2025-05-04T14:02:01+08:00'
tags: [Array, Two Pointers, Dynamic Programming, Stack, Monotonic Stack]
---

## Solution 1

- 參考 [Trapping Rain Water - Neetcode](https://youtu.be/ZI2z5pq0TqA?si=_WI-AGRACoPzBzxf)
- 每一個 index 能承裝的水量，取決於左邊的最高點 maxLeft 和右邊的最高點 maxRight，maxLeft 跟 maxRight 中比較小的值代表是兩邊圍起來的高度。
- 根據上面的定義，可以建立兩個陣列 maxLeft 看 maxRight，分別代表每個 index 的左邊最高點和右邊最高點是多少。
- 最後把全部的 height 跑過一遍，把圍起來的高度 min(maxLeft[i], maxRight[i]) 扣掉 height[i] 就是這個 index 能裝的水，全部加起來就是解答。
- Time: O(N), Space: O(N)

### Implementation

```kotlin
class Solution {
    fun trap(height: IntArray): Int {
        val n = height.size
        val maxLeft = IntArray(n)
        val maxRight = IntArray(n)

        for (i in 1 until n) maxLeft[i] = max(maxLeft[i-1], height[i-1])
        for (i in n-2 downTo 0) maxRight[i] = max(maxRight[i+1], height[i+1])

        var result = 0
        for (i in 0 until n) {
            val water = min(maxLeft[i], maxRight[i]) - height[i]
            if (water > 0) result += water
        }

        return result
    }
}
```

## Solution 2

- 參考 [Trapping Rain Water - Neetcode](https://youtu.be/ZI2z5pq0TqA?si=_WI-AGRACoPzBzxf)
- 優化 Solution 1 空間的做法，就要減少 maxLeft 和 maxRight 的儲存空間。
- 因此可以改用 Two Pointer 的方式記錄兩邊的位置，l 和 r 分別從左右兩端往中間移動，每次移動 maxLeft maxRight 比較小的指針。
- 移動完計算這個 index 的水量  min(maxLeft, maxRight) - height[i]，再更新 maxLeft/maxRight。全部的水量加起來就是解答。
- Time: O(N), Space: O(1)

### Implementation

```kotlin
class Solution {
    fun trap(height: IntArray): Int {
        var (l, r) = 0 to height.lastIndex
        var (maxLeft, maxRight) = height[l] to height[r]
        var result = 0

        while (l < r) {
            if (height[l] < height[r]) {
                result += max(min(maxLeft, maxRight) - height[++l], 0)
                maxLeft = max(maxLeft, height[l])
            } else {
                result += max(min(maxLeft, maxRight) - height[--r], 0)
                maxRight = max(maxRight, height[r])
            }
        }

        return result
    }
}
```
