---
title: 13. Roman To Integer
description:
date: 2024-09-30
tags: [Hash Table, Math, String]
---

## Solution

迭代的時候一次看兩個連續的字元，並且把 4 和 9 的組合直接加入到 Map 裡面，可以稍微減少一點計算時間。
每到一個 index 時，如果目前的羅馬數字比下一個數字小，就表示他是 4 或 9 的類型，但是 index 就要往後移兩格。

### Implementation

```kotlin
class Solution {
    val romanMap = mapOf(
        "I" to 1,
        "V" to 5,
        "X" to 10,
        "L" to 50,
        "C" to 100,
        "D" to 500,
        "M" to 1000,
        "IV" to 4,
        "IX" to 9,
        "XL" to 40,
        "XC" to 90,
        "CD" to 400,
        "CM" to 900
    )

    fun getRomanInt(s: String): Int = romanMap[s] ?: 0

    fun romanToInt(s: String): Int {
        var result = 0
        var i = 0

        while (i < s.lastIndex) {
            val current = s[i].toString()
            val next = s[i+1].toString()

            if (getRomanInt(current) < getRomanInt(next)) {
                val key = "$current$next"
                result += getRomanInt(key)
                i += 2
            } else {
                result += getRomanInt(current)
                i++
            }
        }

        if (i < s.length) result += getRomanInt(s[i].toString())

        return result 
    }
}
```
