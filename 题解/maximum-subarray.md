# 最大子数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-subarray/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组，找到一个具有最大和的子数组，返回其最大和。
 ### 样例说明
 **样例1:**

```
输入：[−2,2,−3,4,−1,2,1,−5,3]
输出：6
解释：符合要求的子数组为[4,−1,2,1]，其最大和为 6。
```

**样例2:**

```
输入：[1,2,3,4]
输出：10
解释：符合要求的子数组为[1,2,3,4]，其最大和为 10。
```
 ### 参考代码
 使用前缀和的方法，计算每个位置为结尾的 subarray 的最大值是多少。
```python
class Solution:
    """
    @param nums: A list of integers
    @return: A integer indicate the sum of max subarray
    """
    def maxSubArray(self, nums):
        #prefix_sum记录前i个数的和，max_Sum记录全局最大值，min_Sum记录前i个数中0-k的最小值
        min_sum, max_sum = 0, -sys.maxsize
        prefix_sum = 0
        
        for num in nums:
            prefix_sum += num
            max_sum = max(max_sum, prefix_sum - min_sum)
            min_sum = min(min_sum, prefix_sum)
            
        return max_sum
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)