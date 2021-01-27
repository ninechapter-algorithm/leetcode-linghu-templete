# 格雷编码
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/gray-code/?utm_source=sc-github-wzz)
 ## 题目描述
 格雷编码是一个二进制数字系统，在该系统中，两个连续的数值仅有一个二进制的差异。

给定一个非负整数 `n` ，表示该代码中所有二进制的总数，请找出其格雷编码顺序。一个格雷编码顺序必须以 `0` 开始，并覆盖所有的 2<sup>n</sup> 个整数。
 ### 样例说明
 **样例 1:**

```
输入: 1
输出: [0, 1]
```

**样例 2:**

```
输入: 2
输出: [0, 1, 3, 2]
解释: 
  0 - 00
  1 - 01
  3 - 11
  2 - 10
```
 ### 参考代码
 最简单的做法是利用位运算. 在 [计算机组成与设计](https://www.amazon.cn/dp/B01174AJ0S/ref=sr_1_1?ie=UTF8&qid=1549795920&sr=8-1&keywords=%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BB%84%E6%88%90%E4%B8%8E%E8%AE%BE%E8%AE%A1+%E7%A1%AC%E4%BB%B6%2F%E8%BD%AF%E4%BB%B6%E6%8E%A5%E5%8F%A3)一书上有介绍. (*或者其他相关书籍也有, 笔者在这本书上看到的*)

一个数字对应的格雷编码的计算方式是: 

- 将其二进制第一位(从高位数)与0异或, 得到的结果为格雷码的第一位
- 之后依次将原数的第i位与生成的格雷码第i-1位做异或运算, 即可得到格雷码的第i位.

递归做法题解见九章算法微博: <http://weibo.com/3948019741/BxXJHiQeN>
```cpp
class Solution {
public:
    /**
     * @param n a number
     * @return Gray code
     */
    vector<int> grayCode(int n) {
        vector<int> result(1 << n);
        for (size_t i = 0; i < (1 << n); i++)
            result[i] = i ^ (i >> 1);
        return result;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)