---
title: 136. Single Number
description:
date: '2025-04-12T13:30:17+08:00'
tags: [Array, Bit Manipulation]
---

## Solution

兩個一樣的數字被 XOR 後的結果是 0，因此把全部的數字全部 XOR 在一起，重複的數字都會抵銷變成 0，剩下單獨的那個數字。

Time: O(N), Space: O(1)

### Implementation

```kotlin
class Solution {
    fun singleNumber(nums: IntArray): Int {
        var ans = 0
        nums.forEach { ans = ans xor it}
        return ans
    }
}
```
