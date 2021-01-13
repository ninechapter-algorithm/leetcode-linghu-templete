# 组合总和 IV
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/backpack-vi/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个都是正整数的数组 `nums`，其中没有重复的数。从中找出所有的和为 `target` 的组合个数。
 ### 样例说明
 
 ### 参考代码
 dp求解，dp[i]表示当前和为i的解法个数
```python
class Solution:
    # @param {int[]} nums an integer array and all positive numbers, no duplicates
    # @param {int} target an integer
    # @return {int} an integer
    def backPackVI(self, nums, target):
        # Write your code here
        dp = [0 for i in xrange(target + 1)]
        dp[0] = 1
        
        for j in xrange(1, target+1):
            for a in nums:
                if j >= a:
                    dp[j] += dp[j - a]

        return dp[target]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)