---
title: 427. Construct Quad Tree
description:
date: '2025-03-09T16:40:32+08:00'
tags: [Array, Divide and Conquer, Tree, Matrix]
---

## Solution

- 使用分治法一直把 grid 切成四半，把左上、左下、右上、右下四個部分再跑一次  createNode()，Base Case 一定是 Leaf 所以可以直接建立 Node。
- 合併時候再檢查這四個部分是否都是 Leaf 而且 Value 一樣，如果這兩個條件復合就把目前的 Node 也設定成 Leaf，不是的話就把上面建立好的 Node 都 assign 給 Parent Node。

Time: `O(logN ^ 2)`, Space: `O(1)`

### Implementation

```kotlin
class Solution {
    fun construct(grid: Array<IntArray>): Node? {
        fun createNode(i: Int, j: Int, size: Int): Node {
            if (size == 1) return Node(grid[i][j] == 1, true)

            val mid = size / 2
            val positions = listOf(0 to 0, 0 to mid, mid to 0, mid to mid)
            val nodes = positions.map { createNode(i + it.first, j + it.second, mid) }

            val isLeaf = checkIsLeaf(nodes)
            val parent = Node(nodes.first().`val`, isLeaf)

            if (!parent.isLeaf) {
                parent.apply {
                    topLeft = nodes[0]
                    topRight = nodes[1]
                    bottomLeft = nodes[2]
                    bottomRight = nodes[3]
                }
            }
            return parent
        }
        
        return createNode(0, 0, grid.size)
    }

    fun checkIsLeaf(nodes: List<Node>): Boolean {
        val value = nodes.first().`val`
        for (node in nodes) {
            if (!node.isLeaf) return false
            if (node.`val` != value) return false
        }
        return true
    }
}
```
