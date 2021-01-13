# 硬币排成线 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/coins-in-a-line-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 有 `n` 个不同价值的硬币排成一条线。两个参赛者轮流从 **左边** 依次拿走 1 或 2 个硬币，直到没有硬币为止。计算两个人分别拿到的硬币总价值，价值高的人获胜。

请判定 **先手玩家** 必胜还是必败?

若必胜, 返回 `true`, 否则返回 `false`.
 ### 样例说明
 **样例 1:**

```
输入: [1, 2, 2]
输出: true
解释: 先手玩家直接拿走两颗硬币即可.
```

**样例 2:**

```
输入: [1, 2, 4]
输出: false
解释: 无论先手拿一个还是两个, 后手可以拿完, 然后总价值更高.
```
 ### 参考代码
 使用九章算法强化班和动态规划专题班中讲到的滚动数组。
时间复杂度为 $O(n)$，额外空间复杂度为 $O(1)$
```python
class Solution:
    """
    @param values: a vector of integers
    @return: a boolean which equals to true if the first player will win
    """
    def firstWillWin(self, values):
        if not values:
            return False
            
        if len(values) <= 2:
            return True
            
        n = len(values)
        
        # dynamic programming
        f = [0] * 3
        prefix_sum = [0] * 3
        f[(n - 1) % 3] = prefix_sum[(n - 1) % 3] = values[n - 1]

        # traverse values in reverse order from n-1 to 0
        for i in range(n - 2, -1, -1):
            prefix_sum[i % 3] = prefix_sum[(i + 1) % 3] + values[i]
            f[i % 3] = max(
                values[i] + prefix_sum[(i + 1) % 3] - f[(i + 1) % 3],
                values[i] + values[i + 1] + prefix_sum[(i + 2) % 3] - f[(i + 2) % 3],
            )
        return f[0] > prefix_sum[0] - f[0]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)