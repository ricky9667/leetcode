---
title: 17. Letter Combinations of a Phone Number
description:
date: 2025-02-25
tags: [Hash Table, String, Backtracking]
---

## Solution

### Implementation

```kotlin
class Solution {
    val letterMap = mapOf(
        '2' to "abc",
        '3' to "def",
        '4' to "ghi",
        '5' to "jkl",
        '6' to "mno",
        '7' to "pqrs",
        '8' to "tuv",
        '9' to "wxyz"
    )

    fun letterCombinations(digits: String): List<String> {
        if (digits == "") return listOf()
        val result = mutableListOf<String>()
        
        fun backtrack(p: Int, str: String) {
            if (p >= digits.length) {
                result.add(str)
                return
            }

            val letters = letterMap[digits[p]] ?: return
            for (letter in letters) {
                backtrack(p + 1, "$str$letter")
            }
        }

        backtrack(0, "")
        return result
    }
}
```
