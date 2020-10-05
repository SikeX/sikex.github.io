---
layout:       post
title:        括号生成
subtitle:     "LeetCode-generateParenthese"
date:         2020-10-02 19:45:00
author:       "Sike"
header-img:   "img/in-post/1001-header-bg.jpg"
header-mask:  0.3
catalog: true
tags:
    - LeetCode
    - 算法
    - dfs
    - 递归
---

## **题目描述**

给出n对括号，请编写一个函数来生成所有的由n对括号组成的合法组合。

例如，给出n=3，解集为：


`"((()))", "(()())", "(())()", "()()()", "()(())"`


**示例1**

## 输入

`1`

## 输出
`["()"]`

**示例2**

## 输入

`2`

## 输出
`["(())","()()"]`

## 思路

回溯法

左子树表示添加左括号

右子树表示添加右括号

条件：

左括号个数必须大于右括号个数

![parentheses](/img/parentheses.png)

## 代码实现

```java
import java.util.*;

public class Solution {
    /**
     *
     * @param n int整型
     * @return string字符串ArrayList
     */
    public ArrayList<String> generateParenthesis (int n) {
        // write code here
        ArrayList<String> res = new ArrayList<String>();

        dfs(res, "", n, 0, 0);

        return res;

    }
    private void dfs(ArrayList<String> res, String path, int n, int lc, int rc){
        if(lc > n || rc > n || rc > lc)
            return;
        else if(lc == n && rc == n){
            res.add(path);
            return;
        }
        else{
            dfs(res, path + "(", n, lc + 1, rc);
            dfs(res, path + ")", n, lc, rc + 1);
        }
    }
}
```
