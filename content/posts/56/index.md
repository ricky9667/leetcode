---
title: 56. Merge Intervals
description:
date: 2024-12-03
tags: [Array, Sorting]
---

## Solution 1

- Time Complexity: O(nlogn), Space Complexity O(n)
- 先把 `intervals` 用 start 排序，排序後的 `sortedIntervals` 按照順序拿出，並放進去 `mergedIntervals` 。如果目前拿到的 interval 的 start ≤ `mergedIntervals` 的 end，代表這兩個 interval 有重疊要合併在一起，那就分別取 start 的 min 和 end 的 max。

### Implementation

```kotlin
class Solution {
    fun merge(intervals: Array<IntArray>): Array<IntArray> {
        val sortedIntervals = intervals.sortedBy { it[0] }
        val mergedIntervals = mutableListOf<IntArray>()
        mergedIntervals.add(sortedIntervals.first())

        for (interval in sortedIntervals) {
            val lastInterval = mergedIntervals.last()
            if (interval[0] > lastInterval[1]) {
                mergedIntervals.add(interval)
            } else {
                val newLastInterval = intArrayOf(
                    min(interval[0], lastInterval[0]),
                    max(interval[1], lastInterval[1])
                )
                mergedIntervals.removeLast()
                mergedIntervals.add(newLastInterval)
            }
        }

        return mergedIntervals.toTypedArray()
    }
}
```

## Solution 2

- Time Complexity: O(n), Space Complexity O(n)
- 先用一個迴圈預處理，把每一個 interval 存到 `arr` 中，`arr[start]` 會對到這個 interval 的 `end` ，如果遇到兩個 start 一樣的 interval 就留 end 比較大的。
- 下一個迴圈把 `arr` 掃過一遍，如果遇到 `arr[i]` 不是 -1，表示目前的 index 有一個 `[i, arr[i]]` 的 interval，這時候就把 interval 更新到 `startIndex`, `endIndex` 兩個暫存的 interval。如果下一個找到的 interval 的 start ≤ `endIndex` ，那表示他跟前一個 interval 重疊了，就把 endIndex 改成新的 arr[i]，否則這個 interval 沒有跟前一個重疊，目前的 startIndex, endIndex 就可以加到 mergedIntervals 裡面。

### Implementation

```kotlin
class Solution {
    fun merge(intervals: Array<IntArray>): Array<IntArray> {
        val size = 10001
        val arr = IntArray(size){ -1 }
        var minIndex = intervals[0][0]

        for (interval in intervals) {
            val (start, end) = interval[0] to interval[1]
            arr[start] = max(arr[start], end)
            minIndex = min(minIndex, start)
        }

        val mergedIntervals = mutableListOf<IntArray>()
        var (startIndex, endIndex) = minIndex to arr[minIndex]

        for (i in 0 until size) {
            if (arr[i] == -1) continue
            if (i > endIndex) {
                mergedIntervals.add(intArrayOf(startIndex, endIndex))
                startIndex = i
            }
            endIndex = max(endIndex, arr[i])
        }

        mergedIntervals.add(intArrayOf(startIndex, endIndex))

        return mergedIntervals.toTypedArray()
    }
}
```
