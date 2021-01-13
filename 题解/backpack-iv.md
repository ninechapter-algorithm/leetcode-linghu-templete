# 背包问题 IV
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/backpack-iv/?utm_source=sc-github-wzz)
 ## 题目描述
 给出 n 个物品, 以及一个数组, `nums[i]`代表第i个物品的大小, 保证大小均为正数并且没有重复, 正整数 `target` 表示背包的大小, 找到能填满背包的方案数。
`每一个物品可以使用无数次`
 ### 样例说明
 **样例1**

```
输入: nums = [2,3,6,7] 和 target = 7
输出: 2
解释:
方案有: 
[7]
[2, 2, 3]
```

**样例2**

```
输入: nums = [2,3,4,5] 和 target = 7
输出: 3
解释:
方案有: 
[2, 5]
[3, 4]
[2, 2, 3]
```
 ### 参考代码
 效率比较高的版本。时间复杂度 $O(n * target)$
```python
class Solution:
    """
    @param nums: an integer array and all positive numbers, no duplicates
    @param target: An integer
    @return: An integer
    """
    def backPackIV(self, nums, target):
        dp = [0] * (target + 1)
        dp[0] = 1
        
        for num in nums:
            for i in range(num, target + 1):
                dp[i] += dp[i - num]

        return dp[target]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)