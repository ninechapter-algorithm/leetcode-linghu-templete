# 吹气球
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/burst-ballons/?utm_source=sc-github-wzz)
 ## 题目描述
 有n个气球，编号为`0`到`n-1`，每个气球都有一个分数，存在`nums`数组中。每次吹气球i可以得到的分数为 `nums[left] * nums[i] * nums[right]`，left和right分别表示`i`气球相邻的两个气球。当i气球被吹爆后，其左右两气球即为相邻。要求吹爆所有气球，得到最多的分数。
 ### 样例说明
 
 ### 参考代码
 区间动态规划
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