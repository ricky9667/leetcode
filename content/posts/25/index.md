---
title: 25. Reverse Nodes in k-Group
description:
date: '2025-06-09T10:50:22+08:00'
tags: [Linked List, Recursion]
---

## Solution

- 使用 [206. Reverse Linked List](https://leetcode.ricky-hu.com/posts/206/) 的方法實作每個 Group 的翻轉，並加入一個 k 記錄要 reverse 幾個節點。
- 外面實作先用 `nextHead` 把 `k` 個節點跑一遍，確認還有剩下 k 個節點以上，並記錄下一個 Group 的起點。
- Reverse 之前先記錄翻轉後的 `head` 和 `tail`，並分別跟前後兩端接在一起，最後將 prev 往後移動一個 Group。
- Time: O(N), Space: O(1)

### Implementation

```kotlin
class Solution {
    fun reverseKGroup(head: ListNode?, k: Int): ListNode? {
        if (k == 1) return head
        val dummy = ListNode(0).also { it.next = head }
        var prev: ListNode? = dummy

        while (prev != null) {
            var nextHead: ListNode? = prev?.next

            for(i in 1..k) {
                if (nextHead == null) return dummy.next
                nextHead = nextHead?.next
            }

            val tail = prev?.next // original head -> reversed tail
            val head = reverseList(tail, k) // reverse list and get its head
            prev?.next = head // connect prev node to current group head
            tail?.next = nextHead // connect current group tail to next head
            prev = tail
        }

        return dummy.next
    }

    private fun reverseList(head: ListNode?, k: Int): ListNode? {
        var current: ListNode? = head
        var next: ListNode? = null
        var count = 0

        while (current != null && count++ < k) {
            val temp = current.next
            current.next = next
            next = current
            current = temp
        }

        return next
    }
}
```
