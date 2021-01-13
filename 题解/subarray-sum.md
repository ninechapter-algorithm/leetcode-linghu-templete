# 子数组之和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/subarray-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组，找到和为 $0$ 的子数组。你的代码应该返回满足要求的子数组的起始位置和结束位置
 ### 样例说明
 **样例 1:**

```
输入: [-3, 1, 2, -3, 4]
输出: [0,2] 或 [1,3]	
样例解释： 返回任意一段和为0的区间即可。
```

**样例 2:**

```
输入: [-3, 1, -4, 2, -3, 4]
输出: [1,5]
```
 ### 参考代码
 用九章算法班里讲过的前缀和

某一段[l, r]的和为0， 则其对应presum[l-1] = presum[r].
presum 为数组前缀和。只要保存每个前缀和，找是否有相同的前缀和即可。
```python
class Solution:
    """
    @param nums: A list of integers
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def subarraySum(self, nums):
        prefix_hash = {0: -1}
        prefix_sum = 0
        for i, num in enumerate(nums):
            prefix_sum += num
            if prefix_sum in prefix_hash:
                return prefix_hash[prefix_sum] + 1, i
            prefix_hash[prefix_sum] = i
            
        return -1, -1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)