# 在排序数组中找最接近的K个数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-k-closest-elements/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个目标数 `target`, 一个非负整数 `k`, 一个按照升序排列的数组 `A`。在`A`中找与`target`最接近的`k`个整数。返回这`k`个数并按照与`target`的接近程度从小到大排序，如果接近程度相当，那么小的数排在前面。
 ### 样例说明
 **样例 1:**

```
输入: A = [1, 2, 3], target = 2, k = 3
输出: [2, 1, 3]
```

**样例 2:**

```
输入: A = [1, 4, 6, 8], target = 3, k = 3
输出: [4, 1, 6]
```
 ### 参考代码
 采用的是二分法 + 双指针
二分法确定一个位置，左侧是 < target，右侧是 >= target
然后用两根指针从中间向两边走，依次找到最接近的 k 个数

与 Java 的版本的小区别是，起始位置是先找到右指针。然后左指针=右指针-1。
```python
class Solution:
    """
    @param A: an integer array
    @param target: An integer
    @param k: An integer
    @return: an integer array
    """
    def kClosestNumbers(self, A, target, k):
        # 找到 A[left] < target, A[right] >= target
        # 也就是最接近 target 的两个数，他们肯定是相邻的
        right = self.findUpperClosest(A, target)
        left = right - 1
    
    	# 两根指针从中间往两边扩展，依次找到最接近的 k 个数
        results = []
        for _ in range(k):
            if self.isLeftCloser(A, target, left, right):
                results.append(A[left])
                left -= 1
            else:
                results.append(A[right])
                right += 1
        
        return results
    
    def findUpperClosest(self, A, target):
        # find the first number >= target in A
        start, end = 0, len(A) - 1
        while start + 1 < end:
            mid = (start + end) // 2
            if A[mid] >= target:
                end = mid
            else:
                start = mid
        
        if A[start] >= target:
            return start
        
        if A[end] >= target:            
            return end
        
        # 找不到的情况
        return len(A)
        
    def isLeftCloser(self, A, target, left, right):
        if left < 0:
            return False
        if right >= len(A):
            return True
        return target - A[left] <= A[right] - target
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)