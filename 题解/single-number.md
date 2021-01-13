# 落单的数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/single-number/?utm_source=sc-github-wzz)
 ## 题目描述
 给出 `2 * n + 1`个数字，除其中一个数字之外其他每个数字均出现两次，找到这个数字。
 ### 样例说明
 **样例 1:**
```
输入：[1,1,2,2,3,4,4]
输出：3
解释：
仅3出现一次
```
**样例 2:**
```
输入：[0,0,1]
输出：1
解释：
仅1出现一次
```

 ### 参考代码
 Given an array of integers, every element appears twice except for one. Find that single one.
考点：
* 异或位运算

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
异或运算具有很好的性质，相同数字异或运算后为0，并且具有交换律和结合律，故将所有数字异或运算后即可得到只出现一次的数字。
```python
class Solution:
    """
   @param A : an integer array
   @return : a integer
   """
    def singleNumber(self, A):
        # write your code here
        ans = 0;
        for x in A:
            ans = ans ^ x
        return ans
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)