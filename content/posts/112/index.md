---
title: 112. Path Sum
description:
date: 2025-01-04
tags: [Tree, Depth-First Search, Breadth-First Search, Binary Tree]
---

## Solution

一直把 targetSum 減掉 root value 遞迴。

### Implementation

```kotlin
class Solution {
    fun hasPathSum(root: TreeNode?, targetSum: Int): Boolean {
        if (root == null) return false
        if (root.left == null && root.right == null) return targetSum == root.`val`

        val leafVal = targetSum - root.`val`
        return hasPathSum(root.left, leafVal) || hasPathSum(root.right, leafVal)
    }
}
```
