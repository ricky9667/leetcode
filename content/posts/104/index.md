---
title: 104. Maximum Depth of Binary Tree
description:
date: 2024-12-31
tags: [Tree, Depth-First Search, Breadth-First Search, Binary Tree]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun maxDepth(root: TreeNode?): Int {
        if (root == null) return 0
        return 1 + max(maxDepth(root.left), maxDepth(root.right))
    }
}
```
