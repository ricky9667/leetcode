---
title: 433. Minimum Genetic Mutation
description:
date: '2025-05-25T13:14:57+08:00'
tags: [Hash Table, String, Breadth-First Search]
---

## Soluton

- 先將 bank 轉換成 HashMap 紀錄每一種 Gene 需要的 mutation 次數，預設值設定為 -1。
- 接下來用一個 Queue 並從 startGene 開始做 BFS，每次拿出一個 gene 之後，把每一個 index 換成 ACTG 四種情況各自跑一遍。如果遇到 bank 存在這個 nextGene，而且這個 nextGene 是在 bankMap 的 mutation 次數是 -1 (還沒有遇到過)，就把他設定為 gene 的 mutation + 1，並且丟到 Queue 裡面繼續 BFS。
- 最後 endGene 在 bankMap 裡面的 mutation 數就是答案，沒有存在則是 -1。
- Time: O(n), Space: O(n)

### Implementation

```kotlin
class Solution {
    fun minMutation(startGene: String, endGene: String, bank: Array<String>): Int {
        val queue = LinkedList<String>()
        val bankMap = bank.associate { it to -1 }.toMutableMap()
        
        bankMap[startGene] = 0
        queue.offer(startGene)

        while (queue.isNotEmpty()) {
            val gene = queue.poll()
            val mutation = bankMap[gene] ?: continue

            for (i in 0..7) {
                val geneCharArray = gene.toCharArray()
                for (choice in listOf('A', 'C', 'G', 'T')) {
                    geneCharArray[i] = choice
                    val nextGene = String(geneCharArray)

                    if (nextGene != gene && bankMap[nextGene] == -1) {
                        bankMap[nextGene] = mutation + 1
                        queue.offer(nextGene)
                    }
                }
            }
        }

        return bankMap[endGene] ?: -1
    }
}
```
