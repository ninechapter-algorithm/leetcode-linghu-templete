# 目标最后位置
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/last-position-of-target/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个升序数组，找到 `target` 最后一次出现的位置，如果没出现过返回 `-1`
 ### 样例说明
 **样例 1：**
```
输入：nums = [1,2,2,4,5,5], target = 2
输出：2
```
**样例 2：**
```
输入：nums = [1,2,2,4,5,5], target = 6
输出：-1
```
 ### 参考代码
 ```python
class Solution:
    # @param {int[]} A an integer array sorted in ascending order
    # @param {int} target an integer
    # @return {int} an integer
    def lastPosition(self, A, target):
        if not A or target is None:
            return -1

        start = 0
        end = len(A) - 1

        while start + 1 < end:
            mid = start + (end - start) // 2

            if A[mid] < target:
                start = mid
            elif A[mid] > target:
                end = mid
            else:
                start = mid
    
        if A[end] == target:
            return end
        elif A[start] == target:
            return start
        else:
            return -1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)