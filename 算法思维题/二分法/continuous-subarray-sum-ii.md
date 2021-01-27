# 连续子数组求和 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/continuous-subarray-sum-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数循环数组（头尾相接），请找出一个连续的子数组，使得该子数组的和最大。输出答案时，请分别返回第一个数字和最后一个数字的值。

如果多个答案，请返回其中任意一个。
 ### 样例说明
 **样例 1:**

```
输入: [3, 1, -100, -3, 4]
输出: [4, 1]
```

**样例 2:**

```
输入: [1,-1]
输出: [0, 0]
```
 ### 参考代码
 分两种情况讨论：

1. 最大数组仍然是中间的某一段
2. 最大数组是去掉了中间的一段之后剩下的部分

第一种情况用传统的最大子数组做法走一遍(参考[题解](https://www.jiuzhang.com/solution/continuous-subarray-sum))。第二种做法稍微想一下就可以证明中间被去掉的那一段是整个数组的 minimum subarray。
所以求一遍 minimum subarray 之后，比较两种情况, 取最优解即可

需要特殊考虑 minimum subarray 是取了所有数的情况。
```python
class Solution:
    """
    @param: A: An integer array
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def continuousSubarraySumII(self, A):
        max_start, max_end, max_sum = self.find_maximum_subarray(A)
        min_start, min_end, min_sum = self.find_maximum_subarray([-a for a in A])
        min_sum = -min_sum  # *-1 after reuse find maximum array
        
        total = sum(A)
        if max_sum >= total - min_sum or min_end - min_start + 1 == len(A):
            return [max_start, max_end]
        
        return [min_end + 1, min_start - 1]
        
    def find_maximum_subarray(self, nums):
        max_sum = -sys.maxsize
        curt_sum, start = 0, 0
        max_range = []
        
        for index, num in enumerate(nums):
            if curt_sum < 0:
                curt_sum = 0
                start = index
            curt_sum += num
            if curt_sum > max_sum:
                max_sum = curt_sum
                max_range = [start, index]
                
        return max_range[0], max_range[1], max_sum
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)