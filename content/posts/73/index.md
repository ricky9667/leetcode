---
title: 73. Set Matrix Zeroes
description:
date: 2024-11-24
tags: [Array, Hash Table, Matrix]
---

## Solution 1

- 先把整個 matrix 掃一遍，如果掃到某一個位置是 0，那把這個位置的 i 和 j 分別加入 `heightZeros` 和 `widthZeros` 兩個陣列。
- 掃完之後再分別看 `heightZeros` 和 `widthZeros` 裡面紀錄哪些橫排和直排有 0，再把 0 分別更新到 matrix 上面。

### Implementation

```kotlin
class Solution {
    fun setZeroes(matrix: Array<IntArray>): Unit {
        val height = matrix.size
        val width = matrix[0].size

        val heightZeros = mutableListOf<Int>()
        val widthZeros = mutableListOf<Int>()

        for (i in 0 until height) {
            for (j in 0 until width) {
                if (matrix[i][j] == 0) {
                    heightZeros.add(i)
                    widthZeros.add(j)
                }
            }
        }

        for (i in heightZeros) {
            for (j in 0 until width) {
                matrix[i][j] = 0
            }
        }

        for (j in widthZeros) {
            for (i in 0 until height) {
                matrix[i][j] = 0
            }
        }
    }
}
```

## Solution 2

- Solution 1 的改良版，目的是為了節省掉存 `heightZeros` 和 `widthZeros` 的空間，改成用 matrix 的第一個直排和橫排存取。
- 直接用 `matrix[0][j]` 和 `matrix[i][0]` 紀錄 0 的直橫排的話，第一個直排和橫排的 0 要在最一開始紀錄是否有 0 存在，但是最後才能更新這兩排的 0。
- 空間複雜度會從 `O(m + n)` 變成 `O(1)`。

### Implementation

```kotlin
class Solution {
    fun setZeroes(matrix: Array<IntArray>): Unit {
        val height = matrix.size
        val width = matrix[0].size

        var firstColHasZero = false
        var firstRowHasZero = false

        for (i in 0 until height) {
            if (matrix[i][0] == 0) {
                firstColHasZero = true
                break
            }
        }

        for (j in 0 until width) {
            if (matrix[0][j] == 0) {
                firstRowHasZero = true
                break
            }
        }

        for (i in 1 until height) {
            for (j in 1 until width) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0
                    matrix[0][j] = 0
                }
            }
        }

        for (i in 1 until height) {
            if (matrix[i][0] != 0) continue
            for (j in 1 until width) {
                matrix[i][j] = 0
            }
        }

        for (j in 1 until width) {
            if (matrix[0][j] != 0) continue
            for (i in 1 until height) {
                matrix[i][j] = 0
            }
        }

        if (firstColHasZero) {
            for (i in 0 until height) {
                matrix[i][0] = 0
            }
        }

        if (firstRowHasZero) {
            for (j in 0 until width) {
                matrix[0][j] = 0
            }
        }
    }
}
```
