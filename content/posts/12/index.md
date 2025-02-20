---
title: 12. Integer To Roman
description:
date: 2024-10-07
tags: [Hash Table, Math, String]
---

## Solution 1

來自過去自己的 Submission。

### Implementation

```kotlin
class Solution {
    fun intToRoman(num: Int): String {
        val romans = "IVXLCDM"
        var x = num
        var r+1
        var r = 0

        while (x > 0) {
            val digit = x % 10
            when (digit) {
                9 -> result += "${romans-> result += "${romanselse -> result += "${romans[r]}".repeat(digit)}" + "${romans[r]}"}" + "${romans[r]}"
                in 5..8 -> result += "${romans[r]}".repeat(digit - 5) + "${romans[r+1]}"
                4 
                
            }
            r += 2
            x /= 10
        }
        
        return result.reversed()
    }
}
```

### Implementation

```kotlin
class Solution {
    fun intToRoman(num: Int): String {
        val romanMap = mapOf(
            1000 to "M",
            900 to "CM",
            500 to "D",
            400 to "CD",
            100 to "C",
            90 to "XC",
            50 to "L",
            40 to "XL",
            10 to "X",
            9 to "IX",
            5 to "V",
            4 to "IV",
            1 to "I"
        )
        val nums = romanMap.keys.toList()
        var x = num
        var result = ""

        for (n in nums) {
            while (n <= x) {
                result += romanMap[n]
                x -= n
            }
        }

        return result
    }
}
```
