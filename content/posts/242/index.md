---
title: 242. Valid Anagram
description:
date: '2025-05-27T18:07:20+08:00'
tags: [Hash Table, String, Sorting]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun isAnagram(s: String, t: String): Boolean {
        if (s.length != t.length) return false

        val letterMap = mutableMapOf<Char, Int>()
        for (i in 0 until s.length) {
            val (si, ti) = s[i] to t[i]
            letterMap[si] = letterMap[si]?.let { it + 1 } ?: 1
            letterMap[ti] = letterMap[ti]?.let { it - 1 } ?: -1
        }

        for (value in letterMap.values) {
            if (value != 0) return false
        }

        return true
    }
}
```
