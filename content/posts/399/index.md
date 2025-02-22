---
title: 399. Evaluate Division
description:
date: '2025-02-22T16:30:17+08:00'
tags: [Array, String, Depth-First Search, Breadth-First Search, Union Find, Graph, Shortest Path]
---

## Solution

- 思路
  - 這題的提示是把每一個代數想成一個 Node，每一個除法結果想成一個 Edge，並且因為除法上下顛倒是會影響結果的，因此這個邊也有方向性。
  - 如果我想知道 `a / c` 而且知道 `a / b` 和 `b / c` 的結果，我就想像成 Node `a` → Node `b` → Node `c` ，並把經過的點相乘後就是結果。
- 實作
  - 因此我們可以先把 `equations` 和 `values` 存到每個 Node 裡面，並且每個 Node 都有一個 `divideMap` 代表這個 Node 除以另一個 Node 的結果，也就是總共的 Edge 數量。
  - 建立好上面的架構後，`queries` 裡面的每個問題都可以從分子的 Node 想辦法 BFS 到分母的 Node，如果走不到就代表沒辦法算出來回傳 -1。
- Time: `O(V + E)`, Space: `O(V + E)`

### Implementation

```kotlin
class Node(val key: String) {
    val divideMap = mutableMapOf<String, Double>()
}

class Solution {
    val nodeMap = mutableMapOf<String, Node>()
    val defaultValue = -1.0

    fun calcEquation(equations: List<List<String>>, values: DoubleArray, queries: List<List<String>>): DoubleArray {
        for (i in 0 until values.size) {
            val (top, bottom) = equations[i][0] to equations[i][1]
            val topNode = getClonedNode(top)
            val bottomNode = getClonedNode(bottom)

            topNode.divideMap[bottom] = values[i]
            bottomNode.divideMap[top] = 1 / values[i]
        }

        val results = DoubleArray(queries.size) { defaultValue }
        for (i in 0 until queries.size) {
            val (top, bottom) = queries[i][0] to queries[i][1]
            results[i] = findDivision(top, bottom)
        }

        return results
    }

    private fun findDivision(top: String, bottom: String): Double {
        if (top !in nodeMap || bottom !in nodeMap) return defaultValue

        val q = LinkedList<Pair<String, Double>>()
        val visited = mutableSetOf<String>()
        q.add(top to 1.0)

        while (!q.isEmpty()) {
            val (key, value) = q.remove()
            if (key == bottom) return value
            if (key in visited) continue

            val node = nodeMap[key] ?: continue
            node.divideMap.forEach { (divideKey, divideValue) ->
                q.add(divideKey to value * divideValue)
            }
            visited.add(key)
        }

        return defaultValue
    }

    private fun getClonedNode(key: String): Node {
        val node = nodeMap[key]?.let { it } ?: Node(key)
        nodeMap[key] = node
        return node
    }
}
```
