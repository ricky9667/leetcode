---
title: 3. Longest Substring Without Repeating Characters
description: 
date: 2024-10-11
tags: [Hash Table, String, Sliding Window]
---

## Solution

建立一個 Set 來存目前的 Sliding Window 有哪些字元，i, 和 j, 分別是 Sliding Window 的兩端。

每次在 Set 裡面多加入一個字元 s[j], 的時候，就一直把 s[i], 從 Set 中並把 i, 往前推一格。結束後再把 s[j], 加入，並計算現在的 substring 長度是不是最長的。

### Implementation

```kotlin
class Solution {
    fun lengthOfLongestSubstring(s: String): Int {
        val charSet = mutableSetOf<Char>()
        var maxLength = 0
        var i = 0
        var j = 0

        while (j < s.length) {
            while (i < j && s[j] in charSet) charSet.remove(s[i++])
            charSet.add(s[j++])
            maxLength = max(maxLength, j - i)
        }

        return maxLength
    }
}
```
