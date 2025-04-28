---
title: 69. Sqrt(x)
description:
date: '2025-04-28T20:21:36+08:00'
tags: [Math, Binary Search]
---

## Solution

- 使用二分搜尋找最接近 `sqrt(x)` 的兩個整數，最後 left 跟 right 絕大多數情況都會差距 1。如果 `sqrt(x) == right` 的話答案就是 right，剩下的情況就會 round 到 left。
- 另外要注意兩件事：
    1. 比較平方的時候不能 `mid * mid == x`，而是要用 `mid == x / mid` 避免 overflow。
    2. 需要先處理 `x = 0` 的情況，不然 `right == x / right` 沒辦法除以 0。

### Implementation

```kotlin
class Solution {
    fun mySqrt(x: Int): Int {
        if (x == 0) return 0
        var (left, right) = 0 to x

        while (right - left > 1) {
            val mid = (left + right) / 2
            if (mid == x / mid) return mid
            if (mid > x / mid) right = mid
            else left = mid
        }

        if (right == x / right) return right
        return left
    }
}
```
