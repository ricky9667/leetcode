---
title: 82. Remove Duplicates from Sorted List II
description:
date: '2025-05-13T21:49:00+08:00'
tags: [Linked List, Two Pointers]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun deleteDuplicates(head: ListNode?): ListNode? {
        val dummy = ListNode(0)
        dummy.next = head
        var (prev, current) = dummy to head

        while (current?.next != null) {
            if (current.`val` == current.next.`val`) {
                current = current.next
                while (prev?.next?.`val` == current?.`val`) current = current?.next
                prev.next = current
            } else {
                prev = prev.next
                current = current.next
            }
        }

        return dummy.next
    }
}
```
