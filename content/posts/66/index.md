---
title: 66. Plus One
description:
date: '2025-05-18T12:36:27+08:00'
tags: [Array, Math]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun plusOne(digits: IntArray): IntArray {
        var i = digits.lastIndex
        digits[i]++

        while (i > 0 && digits[i] > 9) {
            digits[i] -= 10
            digits[--i]++
        }

        if (digits[0] > 9) {
            val digits2 = IntArray(digits.size + 1) { 1 }
            digits[0] -= 10
            for (j in 0 until digits.size) {
                digits2[j+1] = digits[j]
            }
            return digits2
        }

        return digits
    }
}
```
