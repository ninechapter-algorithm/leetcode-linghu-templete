# 打劫房屋
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/house-robber/?utm_source=sc-github-wzz)
 ## 题目描述
 假设你是一个专业的窃贼，准备沿着一条街打劫房屋。每个房子都存放着特定金额的钱。你面临的唯一约束条件是：相邻的房子装着相互联系的防盗系统，且 **当相邻的两个房子同一天被打劫时，该系统会自动报警**。

给定一个非负整数列表，表示每个房子中存放的钱， 算一算，如果今晚去打劫，**在不触动报警装置的情况下**, 你最多可以得到多少钱 。
 ### 样例说明
 **样例 1:**

```
输入: [3, 8, 4]
输出: 8
解释: 仅仅打劫第二个房子.
```

**样例 2:**

```
输入: [5, 2, 1, 3] 
输出: 8
解释: 抢第一个和最后一个房子
```
 ### 参考代码
 使用滚动数组的做法，将每个下标直接 % 3。
时间复杂度 $O(n)$，空间复杂度 $O(1)$
```python
class Solution:
    """
    @param A: An array of non-negative integers
    @return: The maximum amount of money you can rob tonight
    """
    def houseRobber(self, A):
        if not A:
            return 0
        if len(A) <= 2:
            return max(A)
            
        f = [0] * 3
        f[0], f[1] = A[0], max(A[0], A[1])
        
        for i in range(2, len(A)):
            f[i % 3] = max(f[(i - 1) % 3], f[(i - 2) % 3] + A[i])
            
        return f[(len(A) - 1) % 3]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)