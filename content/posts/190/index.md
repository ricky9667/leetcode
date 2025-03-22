---
title: 190. Reverse Bits
description:
date: '2025-03-22T17:28:53+08:00'
tags: [Divide and Conquer, Bit Manipulation]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun reverseBits(n: Int): Int {
        var num = n
        var result = 0
        for (i in 0 until 32) {
            result = (result shl 1) or (num and 1)
            num = num ushr 1
        }
        return result
    }
}
```
