---
title: 392. Is Subsequence
description:
date: 2024-10-21
tags: [Two Pointers, String, Dynamic Programming]
---

## Solution

- `s` 是短的字串，`t` 是長的字串。s 只要比對到對的字元，`si` 就往後一格，`ti` 則是每次比對完，不管有沒有一樣都要往後一格。
- 只要 `si` 或是 `ti` 有一個走到底就表示比完了，如果 `si` 有走完就代表 `s` 每一個字元都有在 `t` 裡面，所以 `si == s.length` 就是結果。

### Implementation

```kotlin
class Solution {
    fun isSubsequence(s: String, t: String): Boolean {
        var si = 0
        var ti = 0

        while (si < s.length && ti < t.length) {
            if (s[si] == t[ti]) si++
            ti++
        }

        return si == s.length
    }
}
```
