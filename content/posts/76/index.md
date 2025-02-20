---
title: 76. Minimum Window Substring
description:
date: 2024-11-14
tags: [Hash Table, String, Sliding Window]
---

## Solution

使用一個 Map 來記錄 `t` 裡面每一個數字還有幾個需要使用掉， `i` 和 `j` 紀錄 Sliding Window 的兩端， `x` 和 `y` 紀錄長度最短的解。

另外使用一個變數 `counter` 紀錄 Map 中還有多少個字母需要被用掉，這樣就不需要一直去檢查 Map 裡面每一個值是不是都歸零。

### Implementation

```kotlin
class Solution {
    fun minWindow(s: String, t: String): String {
        val map = t.groupBy { it }.mapValues { it.value.size }.toMutableMap()
        val length = s.length
        var counter = t.length
        var (i, j) = 0 to 0
        var (x, y) = -1 to length

        fun moveLeftPointer() {
            if (counter == 0 && j - i < y - x) {
                x = i
                y = j
            }

            val leftChar = s[i++]
            if (leftChar in map) {
                map[leftChar]?.let {
                    if (it >= 0) counter++
                    map[leftChar] = it + 1
                }
            }
        }

        fun moveRightPointer() {
            val rightChar = s[j++]
            if (rightChar in map) {
                map[rightChar]?.let {
                    if (it > 0) counter--
                    map[rightChar] = it - 1
                }
            }
        }

        while (i < length || j < length) {
            when {
                j < length && (i == j || counter > 0) -> moveRightPointer()
                else -> moveLeftPointer()
            }
        }

        return when (x) {
            -1 -> ""
            else -> s.substring(x, y)
        }
    }
}
```
