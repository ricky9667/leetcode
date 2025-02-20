---
title: 155. Min Stack
description:
date: 2024-12-10
tags: [Stack, Design]
---

## Solution

- 用兩個 Stack 儲存資料，stack 直接存 push() 進來的值，minStack 則會在 value 進來的時候，選擇 value 和 minStack.top() 中比較小的值存進去 minStack，這樣 minStack.top() 永遠會是 stack 裡面最小的值。
- Reference: https://alrightchiu.github.io/SecondRound/stack-neng-gou-zai-o1qu-de-zui-xiao-zhi-de-minstack.html

### Implementation

```kotlin
class MinStack() {

    private val stack = mutableListOf<Int>()
    private val minStack = mutableListOf<Int>()

    fun push(value: Int) {
        stack.add(value)
        if (minStack.isEmpty() || value < minStack.last()) {
            minStack.add(value)
        } else {
            minStack.add(minStack.last())
        }
    }

    fun pop() {
        stack.removeLast()
        minStack.removeLast()
    }

    fun top(): Int = stack.last()

    fun getMin(): Int = minStack.last()
}
```
