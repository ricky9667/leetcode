---
title: 103. Binary Tree Zigzag Level Order Traversal
description:
date: '2025-05-06T18:33:43+08:00'
tags: [Tree, Breadth-First Search, Binary Tree]
---

## Solution

用兩個 stack 分別存偶數層和奇數層的 node，每個 stack pop 出來之後就把 node.left 或是 node.right push 到另一邊的 stack，等到目前的 stack 空了之後再交換。

### Implementation

```kotlin
class Solution {
    fun zigzagLevelOrder(root: TreeNode?): List<List<Int>> {
        if (root == null) return listOf()

        val result = mutableListOf<List<Int>>()
        val layer = mutableListOf<Int>()
        var stackIndex = 0

        val stacks = Array(2) { mutableListOf<TreeNode>() }
        stacks[0].add(root!!)

        while (stacks[0].isNotEmpty() || stacks[1].isNotEmpty()) {
            val i = stackIndex % 2
            val j = (stackIndex + 1) % 2

            val node = stacks[i].removeLast()
            layer.add(node.`val`)

            if (i == 1) {
                node.right?.let { stacks[j].add(it) }
                node.left?.let { stacks[j].add(it) }
            } else {
                node.left?.let { stacks[j].add(it) }
                node.right?.let { stacks[j].add(it) }
            }

            if (stacks[i].isEmpty()) {
                result.add(layer.toList())
                layer.clear()
                stackIndex++
            }
        }
        
        return result
    }
}
```