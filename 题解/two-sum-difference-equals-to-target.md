# 两数和 - 差等于目标值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/two-sum-difference-equals-to-target/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个排序后的整数数组，找到两个数的 `差` 等于目标值。
你需要返回一个包含两个数字的列表`[num1, num2]`, 使得`num`1与`num2`的差为target，同时`num1`必须小于`num2`。
 ### 样例说明
 例1:
```
输入: nums = [2, 7, 15, 24], target = 5 
输出: [2, 7] 
解释:
(7 - 2 = 5)
```
例2:
```
输入: nums = [1, 1], target = 0
输出: [1, 1] 
解释:
(1 - 1 = 0)
```

 ### 参考代码
 由于数组有序，我们可以用双指针来做
对于双指针i,j,当num[j]-num[i]< target时，说明j太小，于是我们将j++，直到num[j]-num[i] >= target，若num[j]-num[i] > target，我们将i++，若num[j]-num[i] = target说明我们找到答案
```python
class Solution:
    """
    @param nums: an array of Integer
    @param target: an integer
    @return: [index1 + 1, index2 + 1] (index1 < index2)
    """
    def twoSum7(self, nums, target):
        n = len(nums)
        if target < 0:
            target = -target
        j = 0
        for i in range(n):
            if i == j:
                j += 1
            while j < n and nums[j] - nums[i] < target:
                j += 1
            if j < n and nums[j] - nums[i] == target:
                return [nums[i],nums[j]]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)