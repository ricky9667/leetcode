---
title: 30. Substring with Concatenation of All Words
description:
date: 2024-11-09
tags: [Hash Table, String, Sliding Window]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun findSubstring(s: String, words: Array<String>): List<Int> {
        val result = mutableListOf<Int>()
        val wordMapCopy = mutableMapOf<String, Int>()
        val length = s.length
        val wordLength = words[0].length
        val substringLength = wordLength * words.size

        for (word in words) {
            wordMapCopy[word] = (wordMapCopy[word] ?: 0) + 1
        }

        for (i in 0 until length) {
            val wordMap = wordMapCopy.toMutableMap()
            val endIndex = i + substringLength
            if (endIndex > length) break

            for (j in i until endIndex step wordLength) {
                if (j + wordLength > length) break

                val word = s.substring(j, j + wordLength)
                if (!wordMap.containsKey(word)) break

                wordMap[word]?.let {
                    if (it > 1) wordMap[word] = it - 1
                    else if (it == 1) wordMap.remove(word)
                }
            }

            if (wordMap.isEmpty()) result.add(i)
        }

        return result
    }
}
```
