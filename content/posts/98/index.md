---
title: 98. Validate Binary Search Tree
description:
date: 2025-01-27
tags: [Tree, Depth-First Search, Binary Search Tree, Binary Tree]
---

## Solution

### Implementation

```kotlin
class Solution {
    var valid: Boolean = true
    var prev: Int? = null

    fun isValidBST(root: TreeNode?): Boolean {
        traverse(root)
        return valid
    }

    fun traverse(root: TreeNode?) {
        if (root == null) return
        traverse(root.left)
        prev?.let { valid = valid && it < root.`val` }
        prev = root.`val`
        traverse(root.right)
    }
}
```
