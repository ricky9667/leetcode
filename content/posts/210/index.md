---
title: 210. Course Schedule II
description:
date: '2025-06-02T01:04:13+08:00'
tags: [Depth-First Search, Breadth-First Search, Graph, Topological Sort]
---

## Solution

- 這題是 Leetcode 207 的進化版本，除了要確認課程能不能修完，還要給出完成課程的順序，只要是能順利完成的順序都可以。因此做法透過我的 [207. Course Schedule](https://leetcode.ricky-hu.com/posts/207/) 來修改的，可以參考這題的程式碼。
- 這題的做法一樣也使用 DFS，不過在 DFS 的過程中除了把每個課程跑過一遍之後，還要記錄哪些課程可以先修。因此只要能 `return true` 的 `num` 都是課可以修掉的，只要遇到就加到 `courseOrder` 。`courseOrder` 是一個 [LinkedHashSet](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.collections/-linked-hash-set/)，除了可以當一般的 Set 使用（檢查是否有某元素，排除重複元素）之外，他也會留著 add() 元素加入的順序，可以當作 List 和 Set 的混合版。
- 把每一個數字都跑過一次 DFS，過程中就會建立 courseOrder 的順序，如果當中有迴圈而沒辦法修課完畢，就回傳一個空的 Array，成功的話就會在最後 `return courseOrder`。
- Time: `O(V + E)`, Space: `O(V)`

### Implementation

```kotlin
class Solution {
    fun findOrder(numCourses: Int, prerequisites: Array<IntArray>): IntArray {
        val preMap = Array(numCourses) { mutableListOf<Int>() }
        for (item in prerequisites) {
            val (course, prerequisite) = item[0] to item[1]
            preMap[course].add(prerequisite)
        }

        val courseOrder = linkedSetOf<Int>()
        val visited = mutableSetOf<Int>()
        fun dfs(num: Int): Boolean {
            if (num in visited) return false
            if (preMap[num].isEmpty()) {
                courseOrder.add(num)
                return true
            }
            
            visited.add(num)
            for (pre in preMap[num]) {
                if (!dfs(pre)) return false
            }
            visited.remove(num)

            preMap[num].clear()
            courseOrder.add(num)
            return true
        }

        for (course in 0 until numCourses) {
            if (!dfs(course)) return intArrayOf()
        }

        return courseOrder.toIntArray()
    }
}
```
