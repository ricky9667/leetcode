---
title: 211. Design Add and Search Words Data Structure
description:
date: '2025-06-01T16:27:18+08:00'
tags: [String, Depth-First Search, Design, Trie]
---

## Solution

- 題目跟 [208. Implement Trie](https://leetcode.com/problems/implement-trie-prefix-tree/) 相似，不過在 `search()` 的時候的 `word` 裡面包含 `.` 就代表這個位置可以被替換成任何字元。
- 這題我改成使用遞迴方式去實作，每次遞迴就是給 `word` 的 index 和目前走到的 Node，如果遇到 `.` 就把這個 Node 每一個 child 都跑過一遍，只要有任何一個遞迴結果成立就代表可以搜尋到 `word`。

### Implementation

```kotlin
class Node(value: Char) {
    var isWord = false
    val children = mutableMapOf<Char, Node>() 
}

class WordDictionary() {
    val root = Node(' ')

    fun addWord(word: String) {
        var current = root
        for (i in 0 until word.length) {
            val letter = word[i]
            current = current.children.getOrPut(letter) { Node(letter) }
            if (i == word.lastIndex) current.isWord = true
        }
    }

    fun search(word: String): Boolean {
        fun run(index: Int, current: Node): Boolean {
            if (index == word.length) return current.isWord

            val letter = word[index]
            if (letter == '.') {
                for (next in current.children.values) {
                    if (run(index + 1, next)) return true
                }
                return false
            }

            val next = current.children[letter] ?: return false
            return run(index + 1, next)
        }

        return run(0, root)
    }
}
```
