---
title: 19. Remove Nth Node From End of List
description:
date: '2025-05-09T17:54:42+08:00'
tags: [Linked List, Two Pointers]
---

## Solution

- 使用兩個 Pointer 間隔 n 個 node，當快的 Pointer 走到底，慢的就是答案了。
- Time: O(N), Space: O(1)

### Implementation

```kotlin
class Solution {
    fun removeNthFromEnd(head: ListNode?, n: Int): ListNode? {
        val dummy = ListNode()
        dummy.next = head

        var (front, back) = dummy to dummy
        repeat(n) { front = front.next }

        while (front.next != null) {
            front = front.next
            back = back.next
        }

        back.next = back.next.next
        return dummy.next
    }
}
```
