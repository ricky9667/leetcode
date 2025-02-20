---
title: 2825. Make String a Subsequence Using Cyclic Increments
description:
date: 2024-10-29
tags: [Two Pointers, String]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun nextChar(c: Char): Char {
        if (c == 'z') return 'a'
        return (c.toInt() + 1).toChar()
    }

    fun canMakeSubsequence(str1: String, str2: String): Boolean {
        var i = 0
        var j = 0

        while (i < str1.length && j < str2.length) {
            if (str1[i] == str2[j]) j++
            else if (nextChar(str1[i]) == str2[j]) j++
            i++
        }

        return j == str2.length
    }
}
```
