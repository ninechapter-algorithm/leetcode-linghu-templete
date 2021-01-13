# 背包问题 V
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/backpack-v/?utm_source=sc-github-wzz)
 ## 题目描述
 给出 n 个物品, 以及一个数组, `nums[i]` 代表第i个物品的大小, 保证大小均为正数, 正整数 `target` 表示背包的大小, 找到能填满背包的方案数。
`每一个物品只能使用一次`
 ### 样例说明
 给出候选物品集合 `[1,2,3,3,7]` 以及 target `7`
```
结果的集合为:
[7]
[1,3,3]
```
返回 `2`
 ### 参考代码
 带一点优化的动态规划。

- 滚动数组。优化了空间。
- 前缀和。优化了时间。没有必要每次都算到 target 那么多的值。
```python
class Solution:
    """
    @param nums: an integer array and all positive numbers
    @param target: An integer
    @return: An integer
    """
    def backPackV(self, nums, target):
        f = [[0] * (target + 1), [0] * (target + 1)]
        f[0][0] = 1
        n = len(nums)
        prefix_sum = 0
        for i in range(1, n + 1):
            f[i % 2][0] = 1
            prefix_sum += nums[i - 1]
            for j in range(1, min(target, prefix_sum) + 1):
                f[i % 2][j] = f[(i - 1) % 2][j]
                if j >= nums[i - 1]:
                    f[i % 2][j] += f[(i - 1) % 2][j - nums[i - 1]]
        
        return f[n % 2][target]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)