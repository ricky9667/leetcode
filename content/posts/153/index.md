---
title: 153. Find Minimum in Rotated Sorted Array
description:
date: 2024-10-28
tags: [Array, Binary Search]
---

## Solution

這題會給你一個排序好的陣列 `nums`，但是這個陣列可能會位移幾格。假設陣列裡面有 `[1, 2, 3, 4, 5, 6, 7]`，可能會位移成 `[3, 4, 5, 6, 7, 1, 2]`。這題的目的是找出這個陣列裡面最小的數字，在這個情況是 index = 5 的位置，也就是 `1`。

這題可以用二分搜去找到最小的數字，不過判斷的方式會不太一樣，我們可以觀察搜尋時分析往左邊找的情況，和往右邊找的情況。

1. 如果 `nums[m]` 比 `nums[l]` 和 `nums[r]` 大，那我們就會往右半邊搜尋。以下面的情況來看，`6` 比 `3` 和 `2` 大，可以觀察到最小的數字在右半邊。

    ```text
    3 4 5 6 7 1 2
    l     m     r  
    ```

2. 如果 `nums[m]` 比 `nums[l]` 和 `nums[r]` 小，那我們就會往右半邊搜尋。以下面的情況來看，`2` 比 `6` 和 `5` 大，可以觀察到最小的數字在左半邊。

    ```text
    6 7 1 2 3 4 5
    l     m     r  
    ```

那如果陣列沒有動過怎麼辦？如果是正常排序好的話，`nums[m]` 會被夾在 `nums[l]` 和 `nums[r]` 中間，不會符合上面兩種情況。在這個情況下最小的數字一定在最左邊，因此二分搜時會一直往左半邊搜尋，因此以下的程式碼就直接讓他走 `else` 這個區塊，因此下面的 `if` 和 `else` 不會反過因此

到最後結束搜尋時，通常 `nums[l]` 會是最大的數字，`nums[r]` 則會是最小的數字，也就是 `nums[l]` 的下一個。但`nums` 如果沒有位移過，那 `nums[l]` 會是最小的數字， `nums[r]` 會是第二小的數字。因此最後還需要判斷這兩個數字誰比較小，並且回傳最小的數字。

### Implementation

```kotlin
class Solution {
    fun findMin(nums: IntArray): Int {
        var l = 0
        var r = nums.lastIndex

        while (r - l > 1) {
            val m = (l + r) / 2
            if (nums[m] > nums[l] && nums[m] > nums[r]) l = m
            else r = m
        }

        return if (nums[l] > nums[r]) return nums[r] else nums[l]
    }
}
```
