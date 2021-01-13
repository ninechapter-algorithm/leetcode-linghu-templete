# 排序数组中最接近元素
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/closest-number-in-sorted-array/?utm_source=sc-github-wzz)
 ## 题目描述
 在一个排好序的数组 *A* 中找到 *i* 使得 *A[i]* 最接近 *target*
 ### 样例说明
 样例1：
```
输入：[1, 2, 3] ，target = 2
输出： 1.
```
样例2：
```
输入：[1, 4, 6]， target = 3
输出： 1.
```
样例3：
```
输入：[1, 4, 6]，target = 5,
输出： 1 或 2.
```
 ### 参考代码
 利用二分查找的思想即可
```python
class Solution:
    # @param {int[]} A an integer array sorted in ascending order
    # @param {int} target an integer
    # @return {int} an integer
    def closestNumber(self, A, target):
        if not A:
            return -1
        start, end = 0, len(A) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if A[mid] == target:
                return mid
            elif A[mid] > target:
                end = mid
            else:
                start = mid
        if A[end] - target > target - A[start]:
            return start
        else:
            return end
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)