## 题目描述

给一棵二叉树，求出该二叉树最底层最左边的节点。

**样例:**

![image](https://github.com/ninechapter-algorithm/ninechapter-algorithm/blob/master/pictures/%E6%89%BE%E4%BA%8C%E5%8F%89%E6%A0%91%E6%9C%80%E5%BA%95%E5%B1%82%E6%9C%80%E5%B7%A6%E8%BE%B9%E7%9A%84%E8%8A%82%E7%82%B9-%E6%A0%B7%E4%BE%8B.png)

## 解题思路分析

这题有2个做法，一是宽度优先搜索，用每层的第一个节点来更新答案。二是深度优先搜索，当遇到一个节点的深度大于目前维护的最大深度时用这个节点来更新答案。

1.  使用**宽度优先搜索**bfs，用每层的第一个节点更新Ans。时间复杂度O(n)。

2.  使用**深度优先搜索**dfs，当我们第一次访问一个深度为depth的节点x（之前只访问过深度小于depth的节点）时，x一定是depth深度的最左节点，用这个节点更新Ans。即我们维护一个最大深度，当遍历到一个点的深度大于最大深度时，用这个节点来更新答案，并更新最大深度即可。时间复杂度O(n)。

## 参考程序

![image](https://github.com/ninechapter-algorithm/ninechapter-algorithm/blob/master/pictures/%E6%89%BE%E4%BA%8C%E5%8F%89%E6%A0%91%E6%9C%80%E5%BA%95%E5%B1%82%E6%9C%80%E5%B7%A6%E8%BE%B9%E7%9A%84%E8%8A%82%E7%82%B9.%E9%A2%98%E8%A7%A3.png)

更多题解参考：[LintCode/LeetCode 参考答案查询](http://www.jiuzhang.com/solution/find-bottom-left-tree-value/?utm_source=sc-github-lm)

## 面试官角度分析

这道题是一道**简单难度题**，考点是基础数据结构二叉树和在二叉树中的搜索，用bfs和dfs均可。给出正确算法即可达到hire。

## LintCode相关问题

[69. 二叉树的层次遍历](https://www.lintcode.com/problem/binary-tree-level-order-traversal/?utm_source=sc-github-lm)

