# 背包问题 III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/backpack-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定 `n` 种物品, 每种物品都有无限个. 第 `i` 个物品的体积为 `A[i]`, 价值为 `V[i]`.

再给定一个容量为 `m` 的背包. 问可以装入背包的最大价值是多少?
 ### 样例说明
 **样例 1:**

```
输入: A = [2, 3, 5, 7], V = [1, 5, 2, 4], m = 10
输出: 15
解释: 装入三个物品 1 (A[1] = 3, V[1] = 5), 总价值 15.
```

**样例 2:**

```
输入: A = [1, 2, 3], V = [1, 2, 3], m = 5
输出: 5
解释: 策略不唯一. 比如, 装入五个物品 0 (A[0] = 1, V[0] = 1).
```
 ### 参考代码
 类似于最基本的01背包, 我们设定 `f[i][j]` 表示前 `i` 种物品装到容量为 `j` 的背包里, 能获取的最大价值为多少.

比较简单的转移是直接枚举第i种物品取用多少个: `f[i][j] = max{f[i - 1][j - x * A[i]] + x * V[i]}`

但是这样速度较慢, 可以优化成 `f[i][j]` 直接由 `f[i][j - A[i]]` 转移, 并且从小到大枚举 `j`, 这样做的含义就是在已经拿过第 `i` 个物品的之后还可以再拿它. 也就是说: 计算 `f[i][j]` 时, 初始设置为 `f[i - 1][j]`, 然后 `f[i][j] = max(f[i][j], f[i][j - A[i]] + V[i])`

另外, 可以使用滚动数组优化, 使用滚动数组之后也不必要手动设置 `f[i][j] = f[i - 1][j]`, 与01背包使用的滚动数组相反, 这里恰好需要正着枚举容量 `j`, 因而有 `f[j] = max(f[j], f[j - A[i]] + V[i])`
```python
class Solution:
    # @param {int[]} A an integer array
    # @param {int[]} V an integer array
    # @param {int} m an integer
    # @return {int} an array
    def backPackIII(self, A, V, m):
        # Write your code here
        f = [0 for i in xrange(m+1)]
        for (a, v) in zip(A, V):
            for j in xrange(a, m+1):
                if f[j - a] + v > f[j]:
                    f[j] = f[j - a] + v
        return f[m]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)