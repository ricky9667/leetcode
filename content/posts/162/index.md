---
title: 162. Find Peak Element
description:
date: '2025-03-21T17:50:30+08:00'
tags: [Array, Binary Search]
---

## Solution 1

- 用一個迴圈查看每一個值是否比下一個大，是的話目前的值就是 peak。如果不是 peak，迭代到下一個值的時候，就可以確保這個值比上一個值大，只要跟下一個值相比較好，依此類推。跑到最後如果沒有找到 peak，那答案就是最後一個 index。
- Time: `O(n)`, Space: `O(1)`

### Implementation

```kotlin
class Solution {
    fun findPeakElement(nums: IntArray): Int {
        for (i in 0 until nums.lastIndex) {
            if (nums[i] > nums[i + 1]) return i
        }
        return nums.lastIndex
    }
}
```

## Solution 2

- 有點不直覺的二分搜，每次二分搜的邏輯是：
  - Case 1: 如果 `nums[mid]` > `nums[mid + 1]` ，代表 peak 會在左半邊，縮小範圍成 left ~ mid 搜尋。
  - Case 2: 如果 `nums[mid]` < `nums[mid + 1]` ，代表 peak 會在右半邊，縮小範圍成 mid + 1 ~ right 搜尋。
- 為什麼可以透過判斷 mid 和 mid + 1 大小就知道哪一側一定有 peak？
  - 以 Case 1 為例，在 `nums[mid]` > `nums[mid + 1]` 成立的情況下，如果 `nums[mid]` 不是 peak，那就代表 `nums[mid - 1]` > `nums[mid]` 。如果一直都沒有遇到 peak，一直往後延伸到 nums[0]，也可以確保 nums[0] 是 peak，因為根據題目的設定 -1 跟 n 都是最小值。
- Time: `O(logn)`, Space: `O(1)`

感謝我的演算法教練 [Brian Tsai](https://baluteshih.blogspot.com/) 的解析。

### Implementation

```kotlin
class Solution {
    fun findPeakElement(nums: IntArray): Int {
        var (left, right) = 0 to nums.lastIndex
        while (left < right) {
            val mid = (left + right) / 2
            if (nums[mid] > nums[mid + 1]) right = mid
            else left = mid + 1
        }
        return left
    }
}
```