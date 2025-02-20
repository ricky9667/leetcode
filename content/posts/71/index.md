---
title: 71. Simplify Path
description:
date: 2024-12-11
tags: [String, Stack]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun simplifyPath(path: String): String {
        val folders = path.split("/")
        val stack = mutableListOf<String>()

        for (folder in folders) {
            if (folder == "..") {
                stack.removeLastOrNull()
            } else if (folder != "" && folder != ".") {
                stack.add(folder)
            }
        }

        return stack.joinToString(prefix = "/", separator = "/")
    }
}
```
