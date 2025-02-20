---
title: 28. Find the Index of the First Occurrence in a String
description:
date: 2024-10-10
tags: [Two Pointers, String, String Matching]
---

## Solution 1

Kotlin 的語法糖XD

### Implementation

```kotlin
class Solution {
    fun strStr(haystack: String, needle: String): Int = haystack.indexOf(needle)
}
```

## Solution 2

當然不能像上面這樣偷懶，所以還是實作一下XD
作法就是外面一層迴圈 `i` 看 `haystack` 起始點從哪裡開始，每一個 `i` 裡面再跑一個迴圈用 `j` 看 `needle` 的 index，然後比對 `haystack` 從 `i` 開始的字串有沒有跟 `needle` 一樣。
另外 `finalIndex` 的用途是提早結束迴圈，如果 `haystack` 從 `i` 開始算到最後的長度比 `needle` 還小，那不可能會找到相同字串。

### Implementation

```kotlin
class Solution {
    fun strStr(haystack: String, needle: String): Int {
        val finalIndex = haystack.length - needle.length + 1
        
        // i = haystackIndex, j = needleIndex
        for (i in 0 until finalIndex) {
            for (j in 0 until needle.length) {
                if (haystack[i+j] != needle[j]) break
                if (j == needle.lastIndex) return i
            }
        }

        return -1
    }
}
```
