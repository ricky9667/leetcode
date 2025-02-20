---
title: 1768. Merge Strings Alternately
description:
date: 2024-12-03
tags: [Two Pointers, String]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun mergeAlternately(word1: String, word2: String): String {
        var s = ""
        var i = 0

        while (i < word1.length || i < word2.length) {
            if (i < word1.length) s += word1[i]
            if (i < word2.length) s += word2[i]
            i++
        }
        
        return s
    }
}
```
