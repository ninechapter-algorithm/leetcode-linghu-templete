## 题目描述

给定一串数列，求出3个互相不覆盖的长度为k的子串，使其数字总和为最大值。输出的值为三个子串的起始下标。如果有多种解，输出字典序最小的一组

**样例:**
```
输入：[1,2,1,2,6,7,5,1],2     
输出：[0,3,5]
```
## 解题思路分析

首先**预处理前缀和**，使sum[i]代表以第i个数结尾的长度为k的子串和，方便我们之后的计算某个区间的和。

**最朴素的方法**是对三段的起始位置进行遍历，求和，时间复杂度是O(n^3)。

那么如何优化呢？

我们先不考虑下标，只考虑答案最大。如果已知前n个字符中符合题意描述“互相不覆盖的长度为k的子串”的1串最大和为sum_max，那么我们加上当前串的值value，就组成了前n+1个串中符合题意描述的2串最大和，为sum_max+value。

因此，对于第i个位置的求和，我们考虑从[0,i-k]的状态转移，在已知的子串和中加入新的子串，求得从起始到i位的两串最大值。同理，如果我们从后往前做相同处理，可以得到从后往前的i位两串最大值。

换言之，可以考虑将它划分为三个区域[0,i-k] [i,i+k-1][i+k,len)，我们只需要枚举中间的sum[i]，早预处理从左到当前位置的最大前缀和，从右到当前位置的最大后缀和，加起来就必定是当前位置能找到的最大和，遍历一遍就能取得最终解。

## 参考程序

![image](https://github.com/ninechapter-algorithm/ninechapter-algorithm/blob/master/pictures/3%E4%B8%AA%E9%9D%9E%E9%87%8D%E5%A4%8D%E5%AD%90%E6%95%B0%E7%BB%84%E6%9C%80%E5%A4%A7%E5%92%8C.png)

参考程序给出的left和right分别记录从左到第i位和从右到第i位的最大sum的下标，因为题意要字典序最小，所以**在更新right的时候注意符号。**

更多题解可以参考：[LintCode / LeetCode 参考答案查询](http://www.jiuzhang.com/solution/maximum-sum-of-3-non-overlapping-subarrays/?utm_source=sc-github-lm)

## 面试官角度分析

本题是一道**中等难度**的题目，主要考察对动态规划的应用和利用预处理进行优化和节省空间，如果能够想出动态规划的解法，那此题就可以得到hire的评分。

## Lintcode相关问题

[41. 最大子数组](https://www.lintcode.com/problem/maximum-subarray/?utm_source=sc-github-lm)

[722. 最大子数组VI](https://www.lintcode.com/problem/maximum-subarray-vi/?utm_source=sc-github-lm)
