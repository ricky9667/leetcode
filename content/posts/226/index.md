---
title: 226. Invert Binary Tree
description:
date: 2025-01-08
tags: [Tree, Depth-First Search, Breadth-First Search, Binary Tree]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun invertTree(root: TreeNode?): TreeNode? {
        if (root != null) {
            val newLeft = invertTree(root.right)
            val newRight = invertTree(root.left)
            root.apply {
                left = newLeft
                right = newRight
            }
        }
        return root
    }
}
```
