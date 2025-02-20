---
title: 48. Rotate Image
description:
date: 2024-11-22
tags: [Array, Math, Matrix]
---

## Solution

```text
A B C D
E F G H
I J K L
M N O P
```

- 以上面的 4x4 Matrix 來看，會一個長條一個長條旋轉，順序會是從外到內旋轉。因此會先做 ABC → DHL → PON → MIE，再做 F → G → K → J
- 以下使用三個變數，`start` 代表旋轉長條的起點，`end` 代表旋轉長條的終點，`offset` 代表旋轉的數字在長條上的位置。
  - 因此旋轉 (`start` = 0, `end` = 2, `offset` = 1) 就是旋轉 B → H → O → I

### Implementation

```kotlin
class Solution {
    fun rotate(matrix: Array<IntArray>): Unit {
        for (start in 0 until matrix.lastIndex) {
            val end = matrix.lastIndex - start
            for (offset in 0 until (end - start)) {
                val p = matrix[start][start + offset]
                matrix[start][start + offset] = matrix[end - offset][start]
                matrix[end - offset][start] = matrix[end][end - offset]
                matrix[end][end - offset] = matrix[start + offset][end]
                matrix[start + offset][end] = p
            }
        }
    }
}
```
