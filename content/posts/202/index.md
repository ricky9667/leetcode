---
title: 202. Happy Number
description:
date: '2025-06-03T20:19:16+08:00'
tags: [Hash Table, Math, Two Pointers]
---

## Solution

### Implementation

```kotlin
class Solution {
    val happySet = mutableSetOf<Int>()

    fun isHappy(n: Int): Boolean {
        if (n == 1) return true
        if (n in happySet) return false
        happySet.add(n)
        return isHappy(calculate(n))
    }

    private fun calculate(n: Int): Int {
        var num = n
        var result = 0
        while (num > 0) {
            result += (num % 10) * (num % 10)
            num /= 10
        }
        return result
    }
}
```
