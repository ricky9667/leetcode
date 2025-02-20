---
title: 125. Valid Palindrome
description:
date: 2024-10-15
tags: [Two Pointers, String]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun isPalindrome(s: String): Boolean {
        var l = 0
        var r = s.lastIndex

        while (l < r) {
            while (!s[l].isLetter() && !s[l].isDigit()) {
                if (l == r) break
                l++
            }

            while (!s[r].isLetter() && !s[r].isDigit()) {
                if (l == r) break
                r--
            }

            if (s[l].lowercaseChar() != s[r].lowercaseChar()) return false

            l++
            r--
        }

        return true
    }
}
```
