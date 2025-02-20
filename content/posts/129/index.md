---
title: 129. Sum Root to Leaf Numbers
description:
date: 2025-01-19
tags: [Tree, Depth-First Search, Binary Tree]
---

## Solution

遞迴的時候先把上面的數字加好再帶下去。

### Implementation

```cpp
class Solution {
public:
    int sumNumbers(TreeNode* root) {
        return run(root, root->val);   
    }

    int run(TreeNode* root, int val) {
        bool hasLeft = root->left != nullptr;
        bool hasRight = root->right != nullptr;

        if (!hasLeft && !hasRight) {
            return val;
        }

        int sum = 0;
        if (hasLeft) {
            int left = 10 * val + root->left->val;
            sum += run(root->left, left);
        }
        if (hasRight) {
            int right = 10 * val + root->right->val;
            sum += run(root->right, right);
        }

        return sum;
    }
};
```
