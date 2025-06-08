---
title: 206. Reverse Linked List
description:
date: '2025-06-08T17:21:15+08:00'
tags: [Linked List, Recursion]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun reverseList(head: ListNode?): ListNode? {
        var current: ListNode? = head
        var next: ListNode? = null

        while (current != null) {
            val temp = current.next
            current.next = next
            next = current
            current = temp
        }

        return next
    }
}
```
