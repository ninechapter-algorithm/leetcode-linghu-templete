# 搜索区间
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/search-for-a-range/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个包含 *n* 个整数的排序数组，找出给定目标值 *target* 的起始和结束位置。

如果目标值不在数组中，则返回`[-1, -1]`
 ### 样例说明
 例1:
```
输入:
[]
9
输出:
[-1,-1]

```

例2:
```
输入:
[5, 7, 7, 8, 8, 10]
8
输出:
[3, 4]
```

 ### 参考代码
 由于是排序数组，两次二分查找，一个是第一次比target-1大的位置，一个是第一次比他target大的位置。返回即可
```python
class Solution:
    """
    @param A : a list of integers
    @param target : an integer to be searched
    @return : a list of length 2, [index1, index2]
    """
    def searchRange(self, A, target):
        if len(A) == 0:
            return [-1, -1]
        
        start, end = 0, len(A) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] < target:
                start = mid
            else:
                end = mid
        
        if A[start] == target:
            leftBound = start
        elif A[end] == target:
            leftBound = end
        else:
            return [-1, -1]
        
        start, end = leftBound, len(A) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] <= target:
                start = mid
            else:
                end = mid
        if A[end] == target:
            rightBound = end
        else:
            rightBound = start
        return [leftBound, rightBound]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)