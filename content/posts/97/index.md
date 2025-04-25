---
title: 97. Interleaving String
description:
date: '2025-04-25T13:48:40+08:00'
tags: [String, Dynamic Programming]
---

## Solution

- 設定 dp 為「**`s1[0 ~ i]` 跟 `s2[0 ~ j]` 是否能組成 `s3[0 ~ i+j]` 的 Interleaving String**」，dp 會存一個 Boolean 值。
- 設定好之後，計算 dp 就跟走迷宮一樣，每一個座標我們可以看，如果以下任一條件成立 dp 就會是 true：
  - 往上一格也是 true，而且 s3[i+j] == s1[i]
  - 往左一格也是 true，而且 s3[i+j] == s2[j]

### Example

```text
s1 = "aabcc", s2 = "dbbca"
s3 = "aadbbcbcac"

  . a a b c c 
. o o o x x x
d x x o o x x
b x x o o o x
b x x o x o o
c x x o o o x
a x x x x o o
```

### Implementation

- Time: O(N^2), Space: O(N^2)

```kotlin
class Solution {
    fun isInterleave(s1: String, s2: String, s3: String): Boolean {
        val n1 = s1.length
        val n2 = s2.length
        if (n1 + n2 != s3.length) return false

        val dp = Array(n1 + 1) { BooleanArray(n2 + 1) }
        fun getDp(i: Int, j: Int) = if (i < 0 || j < 0) false else dp[i][j]

        for (i in 0..n1) {
            for (j in 0..n2) {
                dp[i][j] = when {
                    i + j == 0 -> true
                    getDp(i - 1, j) && s1[i - 1] == s3[i + j - 1] -> true
                    getDp(i, j - 1) && s2[j - 1] == s3[i + j - 1] -> true
                    else -> false
                }
            }
        }

        return dp[n1][n2]
    }
}
```

### Implementation 2

- Time: O(N^2), Space: O(N)

```kotlin
class Solution {
    fun isInterleave(s1: String, s2: String, s3: String): Boolean {
        val n1 = s1.length
        val n2 = s2.length
        if (n1 + n2 != s3.length) return false

        val dp = BooleanArray(n2 + 1)
        fun getDp(i: Int, j: Int) = if (i < 0 || j < 0) false else dp[j]

        for (i in 0..n1) {
            for (j in 0..n2) {
                if (i + j == 0) dp[j] = true
                else {
                    val isTopInterleave = getDp(i - 1, j) && s1[i - 1] == s3[i + j - 1]
                    val isLeftInterleave = getDp(i, j - 1) && s2[j - 1] == s3[i + j - 1]
                    dp[j] = isTopInterleave || isLeftInterleave
                }
            }
        }

        return dp[n2]
    }
}
```
