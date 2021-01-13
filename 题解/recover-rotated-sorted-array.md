# 恢复旋转排序数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/recover-rotated-sorted-array/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个**旋转**排序数组，在原地恢复其排序。（升序）
 ### 样例说明
 
 ### 参考代码
 Given a rotated sorted array, recover it to sorted array in-place.

Example
[4, 5, 1, 2, 3] -> [1, 2, 3, 4, 5]
```python
class Solution:
    """
    @param nums: The rotated sorted array
    @return:  The recovered sorted array
    """
    def recoverRotatedSortedArray(self, nums):
        nums.sort()
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)