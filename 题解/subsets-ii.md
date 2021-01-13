# 子集 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/subsets-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个可能具有重复数字的列表，返回其所有可能的子集。
 ### 样例说明
 **样例 1：**
```
输入：[0]
输出：
[
  [],
  [0]
]
```
**样例 2：**
```
输入：[1,2,2]
输出：
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```
 ### 参考代码
 九章算法班中的方法
```python
class Solution:
    """
    @param nums: A set of numbers.
    @return: A list of lists. All valid subsets.
    """
    def subsetsWithDup(self, nums):
        nums = sorted(nums)
        subsets = []
        self.dfs(nums, 0, [], subsets)
        return subsets
        
    def dfs(self, nums, index, subset, subsets):
        subsets.append(list(subset))
        
        for i in range(index, len(nums)):
            if i > index and nums[i] == nums[i - 1]:
                continue
            subset.append(nums[i])
            self.dfs(nums, i + 1, subset, subsets)
            subset.pop()
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)