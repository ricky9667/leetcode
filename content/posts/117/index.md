---
title: 117. Populating Next Right Pointers in Each Node II
description:
date: 2025-01-15
tags: [Linked List, Tree, Depth-First Search, Breadth-First Search, Binary Tree]
---

## Solution

使用 BFS 遍歷二元樹，用一個 Queue 來追蹤每一層有哪些 Node。同事記錄 end node 來知道說是不是走到這一排的最後一個，遇到 end 就不需要指到 next() ，並且要就重新記錄下一排的 end 在哪。

### Implementation

```cpp
class Solution {
public:
    Node* connect(Node* root) {
        if (root == nullptr)
            return root;

        queue<Node*> nodes;
        Node* end = root;
        nodes.push(root);

        while (!nodes.empty()) {
            auto current = nodes.front();
            nodes.pop();

            if (current->left != nullptr)
                nodes.push(current->left);
            if (current->right != nullptr)
                nodes.push(current->right);
                
            if (current == end) 
                end = nodes.back();
            else
                current->next = nodes.front();
        }

        return root;
    }
};
```
