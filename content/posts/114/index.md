---
title: 114. Flatten Binary Tree to Linked List
description:
date: 2025-01-15
tags: [Linked List, Stack, Tree, Depth-First Search, Binary Tree,]
---

## Solution

用 pre-order 的方式遍歷樹，並另外用 getFlattenEnd 這個方法回傳攤平後的結尾，處理 root left right 三串合併的各種情況。

### Implementation

```cpp
class Solution {
public:
    void flatten(TreeNode* root) {
        if (root == nullptr) return;
        getFlattenEnd(root);
    }

    TreeNode* getFlattenEnd(TreeNode* root) {
        bool hasLeft = root->left != nullptr;
        bool hasRight = root->right != nullptr;

        if (!hasLeft && !hasRight) {
            return root;
        }

        TreeNode *left = nullptr;
        TreeNode *leftEnd = nullptr;
        TreeNode *right = nullptr;
        TreeNode *rightEnd = nullptr;

        if (hasLeft) {
            left = root->left;
            leftEnd = getFlattenEnd(left);
        }
        if (hasRight) {
            right = root->right;
            rightEnd = getFlattenEnd(right);
        }
        root->left = nullptr;

        if (!hasLeft) {
            root->right = right;
            return rightEnd;
        }
        if (!hasRight) {
            root->right = left;
            return leftEnd;
        }
        root->right = left;
        leftEnd->right = right;
        return rightEnd;
    }
};
```
