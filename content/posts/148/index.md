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

        fun selectLeft() {
            current.next = l
            current = current.next
            l = l?.next
        }

        fun selectRight() {
            current.next = r
            current = current.next
            r = r?.next
        }

        while (l != null || r != null) {
            when {
                l == null -> selectRight()
                r == null -> selectLeft()
                else -> {
                    if (l!!.`val` < r!!.`val`) {
                        selectLeft()
                    } else {
                        selectRight()
                    }
                }
            }
        }

        return dummy.next
    }
}
```
