---
title: 148. Sort List
description:
date: 2025-03-06
tags: [Linked List, Two Pointers, Divide and Conquer, Sorting, Merge Sort]
---

## Solution

Time: `O(nlogn)`
Space: `O(1)`

### Implementation

```kotlin
class Solution {
    fun sortList(head: ListNode?): ListNode? {
        if (head?.next == null) return head

        val left = head
        val leftEnd = getMid(head)
        val right = leftEnd.next
        leftEnd.next = null

        val newLeft = sortList(left)
        val newRight = sortList(right)
        return mergeList(newLeft, newRight)
    }

    fun getMid(head: ListNode): ListNode {
        var (slow, fast) = head to head.next
        while (fast?.next != null) {
            slow = slow.next
            fast = fast.next.next
        }
        return slow
    }

    fun mergeList(left: ListNode?, right: ListNode?): ListNode {
        val dummy = ListNode(0)
        var current = dummy
        var (l, r) = left to right

        while (l != null && r != null) {
            if (l!!.`val` < r!!.`val`) {
                current.next = l
                l = l?.next
            } else {
                current.next = r
                r = r?.next
            }
            current = current.next
        }
        
        if (l == null) current.next = r
        if (r == null) current.next = l

        return dummy.next
    }
}
```
