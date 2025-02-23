---
title: 207. Course Schedule
description:
date: '2025-02-23T15:59:59+08:00'
tags: [tag names]
---

## Solution

- 思路
  - 參考 [Course Schedule - Neetcode](https://youtu.be/EgI5nU9etnU?si=1KesT_mCOjRJNeap)
  - 對每一個 course 建立 preMap，裡面存每個課程有哪些必修課。
  - 接下來對每個 course 做 DFS，每走到一個課程就確認他有哪些必修課。如果是空的代表他沒有其他課擋住，如果不是空的就要把每一個 prerequisite 確認一遍，確認過就把 prerequisite list 清空回傳 true。
  - 如果課程無法被完成，代表 course 裡面有環，因此可以在 DFS 的過程中用一個 Set 去紀錄誰被走過，如果發現這個數字已經在 Set 裡面就是有環 return false。
- Time: `O(V + E)`, Space: `O(V)`

### Implementation

```kotlin
class Solution {
    fun canFinish(numCourses: Int, prerequisites: Array<IntArray>): Boolean {
        val preMap = Array(numCourses) { mutableListOf<Int>() }
        for (item in prerequisites) {
            val (course, prerequisite) = item[0] to item[1]
            preMap[course].add(prerequisite)
        }

        val visited = mutableSetOf<Int>()
        fun dfs(num: Int): Boolean {
            if (num in visited) return false
            if (preMap[num].isEmpty()) return true
            
            visited.add(num)
            for (pre in preMap[num]) {
                if (!dfs(pre)) return false
            }
            
            visited.remove(num)
            preMap[num].clear()
            return true
        }

        for (course in 0 until numCourses) {
            if (!dfs(course)) return false
        }

        return true
    }
}
```
