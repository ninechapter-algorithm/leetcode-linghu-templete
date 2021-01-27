# 打劫房屋 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/house-robber-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 在上次打劫完一条街道之后，窃贼又发现了一个新的可以打劫的地方，**但这次所有的房子围成了一个圈，这就意味着第一间房子和最后一间房子是挨着的**。每个房子都存放着特定金额的钱。你面临的唯一约束条件是：**相邻的房子装着相互联系的防盗系统，且 当相邻的两个房子同一天被打劫时，该系统会自动报警**。

给定一个非负整数列表，表示每个房子中存放的钱， 算一算，如果今晚去打劫，在不触动报警装置的情况下, 你最多可以得到多少钱 。
 ### 样例说明
 **样例1**

```
输入: nums = [3,6,4]
输出: 6
```

**样例2**

```
输入: nums = [2,3,2,3]
输出: 6
```

 ### 参考代码
 动态规划
考虑前若干个房子，记录抢最后一个房子或者不抢最后一个房子能抢到的最多的钱
然后交叉更新
```python
class Solution:
    # @param nums: A list of non-negative integers.
    # return: an integer
    def houseRobber2(self, nums):
        # write your code here
        n = len(nums)
        if n == 0:
            return 0
        if n == 1:
            return nums[0]

        dp = [0] * n
        
        dp[0], dp[1] = 0, nums[1]
        for i in range(2, n):
            dp[i] = max(dp[i - 2] + nums[i], dp[i - 1])

        answer = dp[n - 1]

        dp[0], dp[1] = nums[0], max(nums[0], nums[1])
        for i in range(2, n - 1):
            dp[i] = max(dp[i - 2] + nums[i], dp[i - 1])

        return max(dp[n - 2], answer)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)