# 吹气球
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/burst-balloons/?utm_source=sc-github-wzz)
 ## 题目描述
 有n个气球，编号为`0`到`n-1`，每个气球都有一个分数，存在`nums`数组中。每次吹气球i可以得到的分数为 `nums[left] * nums[i] * nums[right]`，left和right分别表示`i`气球相邻的两个气球。当i气球被吹爆后，其左右两气球即为相邻。要求吹爆所有气球，得到最多的分数。
 ### 样例说明
 **样例 1:**
```
输入：[4, 1, 5, 10]
输出：270
解释：
nums = [4, 1, 5, 10] 吹爆 1, 得分 4 * 1 * 5 = 20
nums = [4, 5, 10]   吹爆 5, 得分 4 * 5 * 10 = 200 
nums = [4, 10]   吹爆 4, 得分 1 * 4 * 10 = 40
nums = [10]   吹爆 10, 得分 1 * 10 * 1 = 10
总得分 20 + 200 + 40 + 10 = 270
```

**样例 2:**
```
输入：[3,1,5]
输出：35
解释：
nums = [3, 1, 5] 吹爆 1, 得分 3 * 1 * 5 = 15
nums = [3, 5] 吹爆 3, 得分 1 * 3 * 5 = 15
nums = [5] 吹爆 5, 得分 1 * 5 * 1 = 5
总得分 15 + 15 + 5  = 35
```

 ### 参考代码
 使用记忆化搜索的方法。
memo[i][j] 表示 burst i+1~j-1 这些气球，留下i,j后的最大收益。
nums 数组需要前后都添加一个1.
```python
class Solution:
    """
    @param nums: A list of integer
    @return: An integer, maximum coins
    """
    def maxCoins(self, nums):
        if not nums:
            return 0

        # [4,1,5] => [1,4,1,5,1]
        nums = [1, *nums, 1]
        return self.memo_search(nums, 0, len(nums) - 1, {})
        
    def memo_search(self, nums, i, j, memo):
        if i == j:
            return 0 
            
        if (i, j) in memo:
            return memo[(i, j)]
        
        best = 0
        for k in range(i + 1, j):
            left = self.memo_search(nums, i, k, memo)
            right = self.memo_search(nums, k, j, memo)
            best = max(best, left + right + nums[i] * nums[k] * nums[j])
        
        memo[(i, j)] = best
        return best
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)