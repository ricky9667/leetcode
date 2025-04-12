---
title: 137. Single Number II
description:
date: '2025-04-12T13:56:10+08:00'
tags: [Array, Bit Manipulation]
---

## Solution

- 迭代整個 `nums` 陣列，`one` 紀錄目前遇到的數字 XOR 起來的值，`two` 紀錄目前遇到的數字兩次 XOR 起來的值。
- `one = (one xor num) and two.inv()`
  - 把目前的數字 xor one 的解，但是 num 如果有在 two 紀錄過，就表示這個數字被遇到第三次了，要從 two 移除，所以 two 有這個數字就會用 and 取消掉。
- `two = (two xor num) and one.inv()`
  - 把目前的數字 xor two 的解，但是 num 如果有在 one 紀錄過，因為執行完上一個步驟，就代表這個數字是第一次遇到不用 XOR 進來，所以 one 有這個數字就會用 and 取消掉。
- 我沒看解答一定不會做：https://ithelp.ithome.com.tw/articles/10242654
- Time: O(N), Space: O(1)

### Implementation

```kotlin
class Solution {
    fun singleNumber(nums: IntArray): Int {
        var one = 0
        var two = 0
        for (num in nums) {
            one = (one xor num) and two.inv()
            two = (two xor num) and one.inv()
        }
        return one
    }
}
```
