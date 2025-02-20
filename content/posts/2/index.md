---
title: 2. Add Two Numbers
description: 
date: 2024-10-11
tags: [Linked List, Math, Recursion]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun addTwoNumbers(l1: ListNode?, l2: ListNode?): ListNode? {
        val head = ListNode(0)
        var current = head
        var (node1, node2) = l1 to l2
        var carry = 0

        fun hasNextDigit() = node1 != null || node2 != null

        while (hasNextDigit()) {
            val v1 = node1?.`val`?.let { it } ?: 0
            val v2 = node2?.`val`?.let { it } ?: 0

            val result = current.`val` + v1 + v2
            current.`val` = result % 10
            carry = result / 10

            node1 = node1?.next
            node2 = node2?.next
            if (hasNextDigit() || carry > 0) {
                current.next = ListNode(carry)
                current = current.next
            }
        }

        return head 
    }
}
```
