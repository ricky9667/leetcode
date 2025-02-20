---
title: 189. Rotate Array
description:
date: 2024-07-27
tags: [Array, Math, Two Pointers]
---

## Solution

觀察 Array 在前後的變化，會發現 k 個數字會搬到前面：

- `k = 3`: `[1, 2, 3, 4, 5, 6, 7]` -> `[5, 6, 7, 1, 2, 3, 4]`

想要達到空間複雜度只有 O(1)，可以用以下方法：

1. Reverse 整個 List，讓後面的數字翻轉到前面。
2. Reverse 前面 `k` 個數字，把前段數字排正。
3. Reverse 後面 `n - k` 個數字，把後段數字排正。

> Note: 因為 `k` 的輸入可能會超過 `n`，因此在計算的時候需要把 `k % n`。

### Example 1

```text=
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
```

1. `[1,2,3,4,5,6,7]` -> `[7,6,5,4,3,2,1]`
2. `[7,6,5,4,3,2,1]` -> `[5,6,7,4,3,2,1]`
3. `[5,6,7,4,3,2,1]` -> `[5,6,7,1,2,3,4]`

### Implementation

```kotlin
class Solution {
    fun rotate(nums: IntArray, k: Int): Unit {
        val n = nums.size
        nums.reverse(0, n)
        nums.reverse(0, k % n)
        nums.reverse(k % n, n)
    }
}
```

### Reference

- [Rotate array (list) in linear time and constant memory - StackOverflow](https://stackoverflow.com/questions/60177936/rotate-array-list-in-linear-time-and-constant-memory)
