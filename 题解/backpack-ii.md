# 背包问题 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/backpack-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 有 `n` 个物品和一个大小为 `m` 的背包. 给定数组 `A` 表示每个物品的大小和数组 `V` 表示每个物品的价值.

问最多能装入背包的总价值是多大?
 ### 样例说明
 **样例 1:**

```
输入: m = 10, A = [2, 3, 5, 7], V = [1, 5, 2, 4]
输出: 9
解释: 装入 A[1] 和 A[3] 可以得到最大价值, V[1] + V[3] = 9 
```

**样例 2:**

```
输入: m = 10, A = [2, 3, 8], V = [2, 5, 8]
输出: 10
解释: 装入 A[0] 和 A[2] 可以得到最大价值, V[0] + V[2] = 10
```
 ### 参考代码
 经典的01背包问题, 资源分配型动态规划.

设定 f[i][j] 表示前 i 个物品装入大小为 j 的背包里, 可以获取的最大价值总和. 决策就是第i个物品装不装入背包, 所以状态转移方程就是 `f[i][j] = max(f[i - 1][j], f[i - 1][j - A[i]] + V[i])`

可以使用滚动数组优化空间至 O(m).
```python
class Solution:
    # @param m: An integer m denotes the size of a backpack
    # @param A & V: Given n items with size A[i] and value V[i]
    def backPackII(self, m, A, V):
        # write your code here
        f = [0 for i in xrange(m+1)]
        n = len(A)
        for i in range(n):
            for j in xrange(m, A[i]-1, -1):
                f[j] = max(f[j] , f[j-A[i]] + V[i])
        return f[m]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)