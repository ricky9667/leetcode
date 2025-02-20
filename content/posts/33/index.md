---
title: 33. Search in Rotated Sorted Array
description:
date: 2024-10-28
tags: [Array, Binary Search]
---

## Solution

這題是 [153. Find Minimum in Rotated Sorted Array](../153/) 的延伸，題目要求變成給你一個 `target`，並且尋找這個排序過且位移的陣列的 `target` 在哪裡，找不到就回傳 `-1`。

我們可以先用 [153. Find Minimum in Rotated Sorted Array](../153/) 裡面的方法二分搜到最小的數字在哪一個位置 `p`。找到之後我們就可以做第二次二分搜，尋找 `p` ~ `p + n` 之間的數字，並且在搜尋過程中取 index % n 的餘數，因為位移後的 index 會超過 n。

### Implementation

```kotlin
class Solution {
    fun search(nums: IntArray, target: Int): Int {
        val n = nums.size
        var l = 0
        var r = nums.lastIndex

        while (r - l > 1) {
            val m = (l + r) / 2
            if (nums[m] > nums[l] && nums[m] > nums[r]) l = m
            else r = m
        }

        if (nums[l] > nums[r]) l = r 
        r = l + n

        while (r - l > 1) {
            val m = (l + r) / 2
            if (nums[m % n] == target) return m % n
            if (nums[m % n] > target) r = m
            else l = m
        }
        
        return if (nums[l % n] == target) l % n else -1
    }
}
```
