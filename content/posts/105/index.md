---
title: 105. Construct Binary Tree from Preorder and Inorder Traversal
description:
date: 2025-01-01
tags: [Array, Hash Table, Divide and Conquer, Tree, Binary Tree]
---

## Solution

- 參考：[Neetcode - Construct Binary Tree from Inorder and Preorder Traversal](https://www.youtube.com/watch?v=ihj4IQGZ2zc)
- 使用遞迴來建造這個二元樹，可以先從 `preorder` 的第一個知道目前的 root 是誰。知道後可以用這個 root 在 `inorder` 中尋找 index 後得知，在 root 左邊的數字是左邊的 sub tree，在 root 右邊的數字是右邊的 sub tree。知道有哪些數字後，就分別對左右兩顆 sub tree 執行 `buildTree()` 並把對應的 `preorder` 和 `inorder` 傳進去。

### Implementation

```kotlin
class Solution {
    fun buildTree(preorder: IntArray, inorder: IntArray): TreeNode? {
        if (preorder.isEmpty()) return null

        val value = preorder[0]
        val node = TreeNode(value)
        val rootIndex = inorder.indexOf(value)

        node.left = buildTree(
            preorder.copyOfRange(1, rootIndex + 1),
            inorder.copyOfRange(0, rootIndex) 
        )

        node.right = buildTree(
            preorder.copyOfRange(rootIndex + 1, preorder.size),
            inorder.copyOfRange(rootIndex + 1, inorder.size)
        )

        return node 
    }
}
```
