---
title: 141. Linked List Cycle
description:
date: 2024-12-17
tags: [Hash Table, Linked List, Two Pointers]
---

## Solution 1

- 用一個 Set 儲存看過的 Node，如果 Set 裡面有出現過就代表有 Cycle，如果先走到底遇到 null 代表沒有。
- Time: O(n), Space: O(n)

### Implementation

```kotlin
class Solution {
    fun hasCycle(head: ListNode?): Boolean {
        val nodeSet = mutableSetOf<ListNode>()
        var current = head

        while (current != null) {
            if (current in nodeSet) return true
            nodeSet.add(current)
            current = current.next
        }

        return false
    }
}
```

## Solution 2

- 指定兩個 Node，first 一次往後跳兩次 next，second 往後跳一次 next。如果有 Cycle 的話 first 就會繞一圈撞到 second，否則會先撞到 null。
- Time: O(n), Space: O(1)

### Implementation

```kotlin
class Solution {
    fun hasCycle(head: ListNode?): Boolean {
        var first = head
        var second = head

        while (first != null && first.next != null && second != null) {
            first = first.next.next
            second = second.next
            if (first == second) return true
        }

        return false
    }
}
```
