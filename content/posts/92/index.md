---
title: 92. Reverse Linked List II
description:
date: 2024-10-11
tags: [Linked List]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun reverseBetween(head: ListNode?, left: Int, right: Int): ListNode? {
        if (left == right) return head
        
        val dummy = ListNode(0)
        dummy.next = head
        var prevNode = dummy

        var index = 0
        var current: ListNode? = dummy

        fun move() {
            index++
            current = current?.next
        }

        while (index < left) {
            prevNode = current!!
            move()
        }

        var leftNode = current
        val rightNode = current
        var nextNode = rightNode
        move()

        while (index <= right) {
            leftNode = current
            move()
            leftNode!!.next = nextNode
            nextNode = leftNode
        }

        prevNode.next = leftNode
        rightNode!!.next = current

        return dummy.next
    }
}
```
