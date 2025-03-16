---
title: 373. Find K Pairs with Smallest Sums
description:
date: '2025-03-16T15:26:58+08:00'
tags: [Array, Heap (Priority Queue)]
---
## Solution

- 使用一個 Priority Queue 儲存 num1 和 num2 的 pair，並且用 sum 來排序。
- 如果直接把 num1 * num2 全部的 pair 加進去空間複雜度會是 O(nm)，測資太多會會 MLE。
- 優化後的方法是每次只加 nums1 裡面最小 (index = 0)的 nums2 的 pair，在拿 Priority Queue 的時候看目前距離 k 還有幾個 item，如果不夠就用目前的 item 中 nums1 的 index + 1, j 加進去 Priority Queue，這樣可以保持 Priority Queue 只有 k 個資料所以操作的時候複雜度會比較小。

Time: `O(klogk)`, Space: `O(k)`

### Implementation

```kotlin
class Solution {
    fun kSmallestPairs(nums1: IntArray, nums2: IntArray, k: Int): List<List<Int>> {
        val pq = PriorityQueue<Triple<Int, Int, Int>>(compareBy { it.first })
        val result = mutableListOf<List<Int>>()

        for (j in 0 until minOf(nums2.size, k)) {
            pq.offer(Triple(nums1[0] + nums2[j], 0, j))
        }

        var count = k
        while (count-- > 0) {
            val (sum, i, j) = pq.poll()
            result.add(listOf(nums1[i], nums2[j]))

            if (i + 1 < nums1.size) {
                pq.offer(Triple(nums1[i + 1] + nums2[j], i + 1, j))
            }
        }

        return result
    }
}
```
