# 拥有同样多的1的下一个数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/next-smaller-and-larger-number-with-the-same-1-bits/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个正整数，找出其用二进制表示拥有同样`1`的数量的比它小的最大正数和比它大的最小正数。

如果找不到则输出`-1`，这里的正整数都是指32位带符号正整数。
 ### 样例说明
 **样例 1:**
```
输入: n=5
输出: Smaller: 3 ,Larger : 6
```
**样例 2:**
```
输入: n=6
输出: Smaller: 5 ,Larger : 9
```
 ### 参考代码
 ```python
class Solution:
    # @param {int} n a 32bit positive integer
    # @return {int} a 32bit positive integer or -1
    def getPrev(self, n):
        # Write your code here
        temp = n;
        c0 = 0;
        c1 = 0;
        while (temp & 1) == 1:
            c1 += 1
            temp >>= 1

        if temp == 0:
            return -1

        while ((temp & 1) == 0) and (temp != 0):
            c0 += 1
            temp >>= 1

        return n - (1 << c1) - (1 << (c0 - 1)) + 1

    # @param {int} n a 32bit positive integer
    # @return {int} a 32bit positive integer or -1
    def getNext(self, n):
        # Write your code here
        temp = n
        c0 = 0
        c1 = 0
        
        while ((temp & 1) == 0) and (temp != 0):
            c0 += 1
            temp >>= 1

        while (temp & 1) == 1:
            c1 += 1
            temp >>= 1

        result = n + (1 << c0) + (1 << (c1 - 1)) - 1;
        if result < 0 or result >= (1 << 31):
            return -1

        return n + (1 << c0) + (1 << (c1 - 1)) - 1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)