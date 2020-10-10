---
layout:       post
title:        "全排列II"
subtitle:     "LeetCode-permutation2"
date:         2020-10-08 19:45:00
author:       "Sike"
header-img:   "img/in-post/1001-header-bg.jpg"
header-mask:  0.3
catalog: true
tags:
    - LeetCode
    - 算法
    - 递归
    - 回溯法
---

# 全排列II(重复元素)

## 题目描述

给定一个可包含重复数字的序列，返回所有不重复的全排列。

## 实例

```
输入: [1,1,2]
输出:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

## 思路
---
大体思路与[没有重复元素的全排列](https://sikex.github.io/2020/10/03/permute/)类似，但是需要去除重复的序列

res记录最后的结果

path用来记录满足条件的序列

used[ ]用来记录元素是否使用过

需要对num数组排序以便进行去重剪枝

当num中有重复元素的时候，只需要考虑一个，但是这是横向考虑，这样的话在迭代的时候肯定会收到影响，所以需要考虑前一个元素是否使用过，如果前一元素没有使用过则代表前一元素是刚回溯上来取消选择了，这时候就需要去重剪枝了。

![permutation2](/img/permutation2.png)

图片来自LeetCode-[liweiwei1419](https://leetcode-cn.com/problems/permutations-ii/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liwe-2/)

---

## 代码实现

```java
import java.util.*;

public class Solution {
	ArrayList<ArrayList<Integer>> res;
    public ArrayList<ArrayList<Integer>> permuteUnique(int[] num) {
    	res = new ArrayList<ArrayList<Integer>>();
        ArrayList<Integer> path = new ArrayList<Integer>();
        boolean[] used = new boolean[num.length];
        if(num.length == 0){
            return res;
        }

        Arrays.sort(num);

        dfs(num, path, used);

        return res;
    }
    private void dfs(int[] num, ArrayList<Integer> path, boolean[] used){
        if(path.size() == num.length){
            res.add(new ArrayList<Integer>(path));
            return;
        }
        for(int i = 0; i < num.length; i++){
            if(used[i]) {
                continue;
            }
            if(i > 0 && num[i] == num[i - 1] && !used[i - 1] ) {
                continue;
            }
            used[i] = true;
            path.add(num[i]);
            dfs(num, path, used);
            //取消选择，向上回溯
            path.remove(path.size() - 1);
            used[i] = false;
        }
    }
}
```
