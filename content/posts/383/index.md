---
title: 383. Ransom Note
description:
date: 2024-11-10
tags: [Hash Table, String, Counting]
---

## Solution

把 `magazine` 的字元加到一個 Map 裡面計算出現次數，再用一個迴圈檢查 `ransomNote`  的每一個字元時，遇到 Map 裡面的字元就 -1。如果不存在字元，或字元的次數被扣到 0 就回傳 `false` ，成功跑完就回傳 `true`。

### Implementation

```kotlin
class Solution {
    fun canConstruct(ransomNote: String, magazine: String): Boolean {
        val map = mutableMapOf<Char, Int>()
        magazine.forEach { map[it] = (map[it] ?: 0) + 1 }

        for (c in ransomNote) {
            val count = map[c] ?: 0
            if (count <= 0) return false
            map[c] = count - 1
        }

        return true
    }
}
```
