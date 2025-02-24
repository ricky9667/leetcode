---
title: 108. Convert Sorted Array to Binary Search Tree
description:
date: '2025-02-24T16:45:34+08:00'
tags: [Array, Divide and Conquer, Tree, Binary Search Tree, Binary Tree]
---

## Solution

Time: `O(N)`, Space: `O(1)`

### Implementation

```kotlin
class Solution {
    fun sortedArrayToBST(nums: IntArray): TreeNode? {
        if (nums.isEmpty()) return null
        val m = nums.size / 2
        return TreeNode(nums[m]).also {
            it.left = sortedArrayToBST(nums.copyOfRange(0, m))
            it.right = sortedArrayToBST(nums.copyOfRange(m + 1, nums.size))
        }
    }
}
```
