---
title: 173. Binary Search Tree Iterator
description:
date: 2025-02-10
tags: [Stack, Tree, Design, Binary Search Tree, Binary Tree, Iterator]
---

## Solution 1

預先把中序遍歷樹把節點都存到一個 List 裡面。
時間複雜度為 `O(n)`，空間複雜度為 `O(n)`。

### Implementation

```kotlin
class BSTIterator(root: TreeNode?) {

    val nodes = mutableListOf<TreeNode>()
    var index = -1

    init {
        traverse(root)
    }
    
    private fun traverse(root: TreeNode?) {
        if (root == null) return
        traverse(root.left)
        nodes.add(root)
        traverse(root.right)
    }

    fun next(): Int = nodes[++index].`val`

    fun hasNext(): Boolean = index != nodes.lastIndex
}
```

## Solution 2

### Implementation

用一個 Stack 維護中序遍歷，每次 pop 一個節點就把那個節點的 right 和 right 後全部的 left 都放入 Stack。
時間複雜度為 `O(1)`，空間複雜度為 `O(h)`。

```kotlin
class BSTIterator(root: TreeNode?) {
    
    val stack = mutableListOf<TreeNode?>()

    init {
        var node = root
        while (node != null) {
            stack.add(node)
            node = node.left
        }
    }

    fun next(): Int {
        val top = stack.removeLast()
        var node = top!!.right
        while (node != null) {
            stack.add(node)
            node = node.left
        }
        return top.`val`
    }

    fun hasNext(): Boolean {
        return stack.isNotEmpty()
    }

}
```
