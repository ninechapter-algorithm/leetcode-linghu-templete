# 交换奇偶二进制位
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/swap-bits/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一个方法，用尽可能少的指令，将一个整数中奇数数位和偶数数位的数字交换 （如，数位 0 和数位 1 交换，数位 2 和数位 3 交换，等等）。
 ### 样例说明
 **样例 1：**
```
输入：0
输出：0
解释：
0 = 0(2) -> 0(2) = 0
```
**样例 2：**
```
输入：5
输出：10
解释：
5 = 101(2) -> 1010(2) = 10
```
 ### 参考代码
 ```cpp
class Solution {
public:
    /**
     * @param x an integer
     * @return an integer
     */
    int swapOddEvenBits(int x) {
        // Write your code here
        return ( ((x & 0xaaaaaaaa) >> 1) | ((x & 0x55555555) << 1) );
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)