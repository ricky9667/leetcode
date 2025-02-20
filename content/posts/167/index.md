---
title: 167. Two Sum II - Input Array Is Sorted
description:
date: 2024-10-13
tags: [Array, Two Pointers, Binary Search]
---

## Solution

單純要過的話，也可以使用 [1. Two Sum](../1/) 用 Hashmap 的做法，不過相信這題不是希望我們練習這個XD

方法跟用 Hashmap 的方法相同的是，會先有一層迴圈看過每一個 `numbers` 裡面的數字，迭代到每個 index 時我們會在陣列中找第二個數字 `currentTarget = target - numbers[index]`，以湊到 `target` 這個值。
由於這題的 `numbers` 陣列是從小到大按照順序排好的，我們可以用**二分搜 Binary Search** 去尋找 `currentTarget`，也就是以下 while 迴圈的部分，如果這次二分搜尋沒有找到，外層的 for 迴圈就可以往下一個數字去找。

### Implementation

```kotlin
class Solution {
    fun twoSum(numbers: IntArray, target: Int): IntArray {
        var firstIndex = -1
        var secondIndex = -1

        for (index in 0 until numbers.size) {
            val currentTarget = target - numbers[index]
            var l = index + 1
            var r = numbers.size

            while (l < r) {
                val m = (l + r) / 2
                if (currentTarget == numbers[m]) {
                    firstIndex = index
                    secondIndex = m
                    break
                } else {
                    if (currentTarget > numbers[m]) l = m + 1
                    else r = m
                }
            }

            if (l < numbers.size && currentTarget == numbers[l]) {
                firstIndex = index
                secondIndex = l
            }

            if (firstIndex != -1 && secondIndex != -1) break
        }

        return intArrayOf(firstIndex + 1, secondIndex + 1)
    }
}
```
