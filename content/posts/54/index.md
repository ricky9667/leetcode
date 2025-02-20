---
title: 54. Spiral Matrix
description:
date: 2024-11-18
tags: [Array, Matrix, Simulation]
---

## Solution

### Implementation

```kotlin
class Solution {
    fun spiralOrder(matrix: Array<IntArray>): List<Int> {
        val result = mutableListOf<Int>()
        var (topEdge, bottomEdge) = 1 to matrix.lastIndex
        var (leftEdge, rightEdge) = 0 to matrix[0].lastIndex
        var (i, j) = 0 to 0
        var direction = 0 // 0 = right, 1 = down, 2 = left, 3 = up

        fun canMove(): Boolean {
            return when (direction) {
                0 -> j + 1 <= rightEdge
                1 -> i + 1 <= bottomEdge
                2 -> j - 1 >= leftEdge
                else -> i - 1 >= topEdge
            }
        }

        fun move() {
            when (direction) {
                0 -> j++
                1 -> i++
                2 -> j--
                else -> i--
            }
        }

        result.add(matrix[i][j])
        while (result.size < matrix.size * matrix[0].size) {
            while (canMove()) {
                move()
                result.add(matrix[i][j])
            }
            
            when (direction) {
                0 -> rightEdge--
                1 -> bottomEdge--
                2 -> leftEdge++
                else -> { 
                    topEdge++
                    direction -= 4
                }
            }
            direction++
        }

        return result
    }
}
```
