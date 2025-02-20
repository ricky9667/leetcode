---
title: 530. Minimum Absolute Difference in BST
description:
date: 2025-01-22
tags: [Tree, Depth-First Search, Breadth-First Search, Binary Search Tree, Binary Tree]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun getMinimumDifference(root: TreeNode?): Int {
        var result = Int.MAX_VALUE
        var lastValue: Int? = null

        fun traverse(node: TreeNode?) {
            if (node == null) return

            traverse(node.left)
            if (lastValue != null)
                result = min(result, node.`val` - lastValue!!)
            lastValue = node.`val`
            traverse(node.right)
        }

        traverse(root)

        return result
    }
}
```
