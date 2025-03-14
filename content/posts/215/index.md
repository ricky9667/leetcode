---
title: 215. Kth Largest Element in an Array
description:
date: '2025-03-14T18:25:52+08:00'
tags: [Array, Divide and Conquer, Sorting, Heap (Priority Queue), Quickselect]
---

## Solution

使用 Quick Sort 的 Partition 演算法 (Quick Select)，選擇一個 Pivot 後，把比這個數字大的丟到他的左邊，小的丟到右邊。丟完之後看 k 的位置，如果 k 在 pivot 左邊就是跑 pivot 左邊的 Quick Select，k 在右邊就跑右邊的 Quick Select，如果剛好是 k 的話就是答案了。

Time: `O(nlogn)`, Space: `O(1)`

### Implementation

```kotlin
class Solution {
    fun findKthLargest(nums: IntArray, k: Int): Int {
        val target = k - 1

        fun quickSelect(left: Int, right: Int): Int {
            val pivot = nums[right]
            var i = left - 1

            for (j in left..right) {
                if (nums[j] >= pivot) {
                    i++
                    nums[i] = nums[j].also { nums[j] = nums[i] }
                }
            }

            if (i == target) return nums[i]
            return if (i < target) quickSelect(i + 1, right) else quickSelect(left, i - 1)
        }

        return quickSelect(0, nums.lastIndex)
    }
}
```
