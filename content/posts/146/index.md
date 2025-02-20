---
title: 146. LRU Cache
description:
date: 2024-12-28
tags: [Hash Table, Linked List, Design, Doubly-Linked List]
---

## Solution 1

實作雙向的 Linked List 並用 dummy start & end node 管理。使用過就用 `removeNode()` + `insertNodeAtStart()` 重新插入到最前面。超過 capacity 就用 `removeNode()` 並從 map 中移除。

### Implementation

```kotlin
class LRUCache(capacity: Int) {

    val maxSize = capacity
    val map = mutableMapOf<Int, Node>()
    val start: Node = Node(0, 0)
    var end: Node = Node(0, 0)

    init {
        start.next = end
        end.prev = start
    }

    fun get(key: Int): Int {
        val node = map[key] ?: return -1

        removeNode(node)
        insertNodeAtStart(node)
        return node.value
    }

    fun put(key: Int, value: Int) {
        if (key in map) {
            val node = map[key] ?: return
            node.value = value
            removeNode(node)
            insertNodeAtStart(node)
        } else {
            val node = Node(key, value)
            map[key] = node
            insertNodeAtStart(node)

            if (map.keys.size > maxSize) {
                end.prev?.let { lruNode ->
                    removeNode(lruNode)
                    map.remove(lruNode.key)
                }
            }
        }
    }

    private fun removeNode(node: Node) {
        val (prev, next) = node.prev to node.next
        prev?.let { it.next = next }
        next?.let { it.prev = prev }
    }

    private fun insertNodeAtStart(node: Node) {
        val next = start.next
        start.next = node
        node.prev = start
        node.next = next
        next?.let { it.prev = node }
    }
}

class Node(val key: Int, var value: Int) {
    var next: Node? = null
    var prev: Node? = null
}
```

### Solution 2

使用 Kotlin 的 [LinkedHashMap](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.collections/-linked-hash-map/) 就能保留資料進入 Map 的順序，這題就變超級簡單了 :D

### Implementation

```kotlin
class LRUCache(capacity: Int) {

    val maxSize = capacity
    val map = linkedMapOf<Int, Int>()

    fun get(key: Int): Int {
        val value = map[key] ?: return -1
        map.remove(key)
        map[key] = value
        return value
    }

    fun put(key: Int, value: Int) {
        map.remove(key)
        map[key] = value
        if (map.size > maxSize) {
            map.remove(map.keys.first())
        }
    }
}
```
