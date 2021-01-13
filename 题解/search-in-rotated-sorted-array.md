# 搜索旋转排序数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/search-in-rotated-sorted-array/?utm_source=sc-github-wzz)
 ## 题目描述
 假设有一个排序的按未知的旋转轴旋转的数组(比如，`0 1 2 4 5 6 7` 可能成为`4 5 6 7 0 1 2`)。给定一个目标值进行搜索，如果在数组中找到目标值返回数组中的索引位置，否则返回-1。你可以假设数组中不存在重复的元素。
 ### 样例说明
 例1:
```
输入: [4, 5, 1, 2, 3] and target=1, 
输出: 2.
```
例2:
```
输入: [4, 5, 1, 2, 3] and target=0, 
输出: -1.
```

 ### 参考代码
 用一次二分法（按照九章算法课上的讲法）。
```
[[python]]
class Solution:
    """
    @param A: an integer rotated sorted array
    @param target: an integer to be searched
    @return: an integer
    """
    def search(self, A, target):
        if not A:
            return -1
            
        start, end = 0, len(A) - 1
        while start + 1 < end:
            mid = (start + end) // 2
            if A[mid] >= A[start]:
                if A[start] <= target <= A[mid]:
                    end = mid
                else:
                    start = mid
            else:
                if A[mid] <= target <= A[end]:
                    start = mid
                else:
                    end = mid
                    
        if A[start] == target:
            return start
        if A[end] == target:
            return end
        return -1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)