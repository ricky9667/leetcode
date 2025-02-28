---
title: 208. Implement Trie (Prefix Tree)
description:
date: '2025-02-28T16:00:06+08:00'
tags: [Hash Table, String, Design, Trie]
---

## Solution

- **Description**
  - 參考[資料結構筆記 - Trie](https://hackmd.io/@blackdiz/rJmA9n-PL)
  - 把每一個字元視為一個 Node，並且每個 Node 裡面用一個 Map 紀錄下一個字元是什麼，讓這一些字成為一顆樹。另外再用一個 Boolean `isWord` 紀錄目前的字元從 root 開始到這裡是不是一個輸入進來的字。
  - 搜尋的時候就從 root 開始往下搜尋就能知道某個 word 或 prefix 是否存在。
- **Complexity**
  - Time: O(M) (insert, search)
  - Space: O(NM)
  - N = number of words, M = length of a word

### Implementation

```kotlin
class Node(value: Char) {
    var isWord = false
    val children = mutableMapOf<Char, Node>() 
}

class Trie() {
    val root = Node(' ')

    fun insert(word: String) {
        var current = root
        var i = 0

        while (i < word.length) {
            val letter = word[i]
            current = current.children.getOrPut(letter) { Node(letter) }

            if (i++ == word.lastIndex) {
                current.isWord = true
            }
        }
    }

    fun search(word: String): Boolean {
        var current = root
        var i = 0

        while (i < word.length) {
            val letter = word[i++]
            current = current.children[letter] ?: return false
        }
        return current.isWord
    }

    fun startsWith(prefix: String): Boolean {
        var current = root
        var i = 0

        while (i < prefix.length) {
            val letter = prefix[i++]
            current = current.children[letter] ?: return false
        }

        return true
    }
}
```
