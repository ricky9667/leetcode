---
title: 649. Dota2 Senate
description:
date: '2025-06-22T15:25:45+08:00'
tags: [String, Greedy, Queue]
---

## Solution

- 兩個隊伍 Radiant 和 Dire 輪流投票，按照 `senate` 的順序，每次投票可以把一個對方隊伍的人踢出，剩下的隊伍就會獲勝。
- 使用兩個 Queue 分別記錄 Radiant 和 Dire 的 index 順序。接下來把兩個 Queue 的第一個 Pop 出來，比較小的 Index 代表他會先被輪到可以踢掉對方，所以只把 Index 小的加回去 Queue，加回去 Queue 的時候要加上 `senate.length` 當作繞一圈之後的順序。
- Time: O(N), Space: O(N)

### Code

```kotlin
class Solution {
    fun predictPartyVictory(senate: String): String {
        val radiant = LinkedList<Int>()
        val dire = LinkedList<Int>()
        val n = senate.length

        for (i in 0 until n) {
            if (senate[i] == 'R') radiant.add(i)
            else dire.add(i)
        }

        while (radiant.isNotEmpty() && dire.isNotEmpty()) {
            val r = radiant.remove()
            val d = dire.remove()

            if (r < d) radiant.add(r + n)
            else dire.add(d + n)
        }

        return if (dire.isEmpty()) "Radiant" else "Dire"
    }
}
```
