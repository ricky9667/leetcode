---
title: 6. Zigzag Conversion
description: 
date: 2024-10-07
tags: [String]
---

## Solution

建立一個 `strList`，並把 Zigzag 的每一行分別存到這個 `strList` 裡面。
可以觀察出來每一個 Zigzag 一輪回來會經過 `(numRows - 1) * 2` 個字元，我們先把它定義為一個 `round`。
如果用 index 看 `numRows = 3` 的例子就是：

```text
0   4   8 ...
1 3 5 7 9 ...
2   6   10 ...
```

可以看出每一輪 `round` 中：

- 如果 index 在 `0` ~ `numRows - 1`，那就是 Zigzag 折返之前的情況，會被列在第 `index % round` 行。
- 如果 index 在 `numRows` 之後，那就是 Zigzag 折返後的情況，會被列在第 `round - (index % round)` 行。

因此我們根據 `index ％ round` 的餘數算出要加在 `strList` 的哪一行，最後再把 `strList` 的字串按照順序加起來就是答案了。
另外 `numRows` 如果是 `1`，那只會有一行，`s` 就是解答，可以直接回傳 `s`。

### Implementation

```kotlin
class Solution {
    fun convert(s: String, numRows: Int): String {
        if (numRows == 1) return s

        var strList = MutableList(numRows) { "" }
        val round = (numRows - 1) * 2

        for (i in 0 until s.length) {
            val line = i % round
            if (line <= numRows - 1) {
                strList[line] += s[i].toString()
            } else {
                strList[round - line] += s[i].toString()
            }
        }

        var result = ""
        strList.forEach {  result += it  }

        return result
    }
}
```
