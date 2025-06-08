---
title: 61. Rotate List
description:
date: '2025-06-08T14:40:36+08:00'
tags: [Linked List, Two Pointers]
---

## Solution

- 首先要確認整個 Linked List 的總長度 `n` 是多少，因此第一個迴圈先把整個 Linked List 跑過一遍。
- 我們其實不需要去一個一個把節點 Rotate 到最前面，我們只要知道要 Rotate 幾個，再從新的節點切斷就好了。因此知道長度是多少之後，我們用第二個迴圈找到切點在哪，切點右邊是 rotate 後的 `newHead`，而左邊是 `newEnd`。
- 最後把舊的尾跟舊的頭接起來，新的尾下一個為 null，再 return 新的頭就是答案。
- Time: O(N), Space: O(1)

### Code

```kotlin
class Solution {
    fun rotateRight(head: ListNode?, k: Int): ListNode? {
        if (head == null || k == 0) return head

        var oldEnd = head
        var n = 1
        while (oldEnd?.next != null) {
            oldEnd = oldEnd.next
            n++
        }

        val newHeadIndex = (n - (k % n)) % n
        if (n == 1 || newHeadIndex == 0) return head
        
        var newEnd = head
        repeat(newHeadIndex - 1) { newEnd = newEnd?.next }
        val newHead = newEnd?.next

        oldEnd.next = head
        newEnd?.next = null

        return newHead
    }
}
```
