---
title: 139. Word Break
description:
date: '2025-04-01T16:20:01+08:00'
tags: [Array, Hash Table, String, Dynamic Programming, Trie, Memoization]
---

## Solution

建立一個 Bool Array dp，紀錄在目前這個 index 是否能用 wordDict裡面的字組成。接下來把 s 的每個依序往後跑，每一次都會 loop 過 wordDict 每個字，如果這個字完全貼合在目前的 index 上，就把 index + word.length 也改成 true，最後一個 index 就會是答案了。

### Implementation

```kotlin
class Solution {
    fun wordBreak(s: String, wordDict: List<String>): Boolean {
        val dp = BooleanArray(s.length + 1)
        dp[0] = true

        for (index in 0 until dp.size) {
            if (!dp[index]) continue
            val substr = s.substring(startIndex = index)

            for (word in wordDict) {
                val nextIndex = index + word.length
                if (nextIndex >= dp.size) continue
                if (substr.startsWith(word)) dp[nextIndex] = true
            }
        }

        return dp.last()
    }
}
```
