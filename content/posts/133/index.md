---
title: 133. Clone Graph
description:
date: 2025-02-20
tags: [Hash Table, Depth-First Search, Breadth-First Search, Graph]
---

## Solution

- 遍歷原本的圖需要把每一個 node 以及 node 有哪些 neighbor 看過一遍，因此用一個 `queue` 來維護 BFS 走過哪些點，並用一個 Set `visited` 來確認每個 node 有沒有走過。
- 另外使用一個 map 來紀錄數字對應到 clone 過的 node，這樣跑到一個新的 node 就把建立的 node 存在 map 裡面，遇到數字可以直接存取。

Time: `O(V + E)`, Space: `O(V)`

### Implementation

```kotlin
class Solution {
    private val cloneMap = mutableMapOf<Int, Node>()

    fun cloneGraph(node: Node?): Node? {
        val queue = LinkedList<Node>()
        val visited = mutableSetOf<Int>()

        node?.let { queue.add(it) }
        while (!queue.isEmpty()) {
            val current = queue.remove()
            val currentVal = current.`val`
            if (currentVal in visited) continue
            val currentClone = getClonedNode(currentVal)

            for (neighbor in current.neighbors) {
                val neighborVal = neighbor?.`val`?.let { it } ?: continue
                val neighborClone = getClonedNode(neighborVal)
                queue.add(neighbor)
                currentClone.neighbors.add(neighborClone)
                visited.add(neighborVal)
            }
        }

        return cloneMap[1]
    }

    private fun getClonedNode(value: Int): Node {
        val node = cloneMap[value]?.let { it } ?: Node(value)
        cloneMap[value] = node
        return node
    }
}
```
