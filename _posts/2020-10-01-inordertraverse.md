---
layout:       post
title:        树的中序遍历
subtitle:     "LeetCode-inorderTraversal"
date:         2020-10-01 19:45:00
author:       "Sike"
header-img:   "img/in-post/1001-header-bg.jpg"
header-mask:  0.3
catalog: true
tags:
    - LeetCode
    - 树
    - 递归
---

# 二叉树的中序遍历

Tags: LeetCode, 树, 递归
date: Oct 1, 2020

## 思路

### 递归算法

想清楚递归边界是什么，在什么时候开始回溯

### 非递归算法

大佬提供的颜色算法，可以很好的解决二叉树的遍历问题

### 代码实现

递归代码

```java
import java.util.*;

/*
 * public class TreeNode {
 *   int val = 0;
 *   TreeNode left = null;
 *   TreeNode right = null;
 * }
 */

public class Solution {
    /**
     *
     * @param root TreeNode类
     * @return int整型ArrayList
     */
    public ArrayList<Integer> inorderTraversal (TreeNode root) {
        // write code here
        ArrayList<Integer> res = new ArrayList<>();
        if(root == null)
            return res;
        else
            inorder(root, res);
        return res;
    }
    private void inorder(TreeNode node, ArrayList<Integer> res){
        if(node != null){
            inorder(node.left,res);
            res.add(node.val);
            inorder(node.right,res);
        }
    }
}
```

 非递归代码

```java
import java.util.*;

/*
 * public class TreeNode {
 *   int val = 0;
 *   TreeNode left = null;
 *   TreeNode right = null;
 * }
 */

public class Solution {
    /**
     *
     * @param root TreeNode类
     * @return int整型ArrayList
     */
    public ArrayList<Integer> inorderTraversal (TreeNode root) {
        // write code here
        Stack<TreeNode> stack = new Stack<TreeNode>();
        ArrayList<Integer> res = new ArrayList<Integer>();
        HashMap<TreeNode, Integer> map = new HashMap<TreeNode,Integer>();

        if(root == null)
            return res;
        stack.push(root);
        map.put(root,1);

        while(!stack.isEmpty()){
            TreeNode node = stack.pop();
            if(map.get(node) == 1){
                if(node.right != null){
                    stack.push(node.right);
                    map.put(node.right,1);
                }
                stack.push(node);
                map.put(node,2);
                if(node.left != null){
                    stack.push(node.left);
                    map.put(node.left, 1);
                }
            }
            else
                res.add(node.val);

        }
        return res;
    }
}
```
