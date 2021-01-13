# K 个有序数组的中位数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/median-of-k-sorted-arrays/?utm_source=sc-github-wzz)
 ## 题目描述
 有 `k` 个有序数组 `nums`。找到这 `k` 个有序数组的中位数。
 ### 样例说明
 **样例 1:**
```
输入:
[[1],[2],[3]]
输出:
2.00
```

**样例 2:**
```
输入:
[[1,1,2],[2,4,8],[3,7,10,20]]
输出:
3.50
```
 ### 参考代码
 使用二分答案的方法。
可以在《九章算法强化班》中学到哦！
```python
class Solution:
    """
    @param nums: the given k sorted arrays
    @return: the median of the given k sorted arrays
    """
    def findMedian(self, nums):
        if not nums:
            return 0.0
            
        n = sum(len(arr) for arr in nums)
        if n == 0:
            return 0.0
            
        if n % 2 == 1:
            return self.find_kth(nums, n // 2 + 1) * 1.0
        return (self.find_kth(nums, n // 2) + self.find_kth(nums, n // 2 + 1)) / 2.0

    # k is one-based, from 1 to n
    def find_kth(self, arrs, k):
        start, end = self.get_range(arrs)
        
        # find the first num that there are >= k nums <= num
        while start + 1 < end:
            mid = (start + end) // 2
            if self.get_smaller_or_equal(arrs, mid) >= k:
                end = mid
            else:
                start = mid
        if self.get_smaller_or_equal(arrs, start) >= k:
            return start
        return end
            
    def get_range(self, arrs):
        start = min(arr[0] for arr in arrs if len(arr))
        end = max(arr[-1] for arr in arrs if len(arr))
        return start, end
        
    def get_smaller_or_equal(self, arrs, val):
        count = 0
        for arr in arrs:
            count += self.get_smaller_or_equal_in_arr(arr, val)
        return count
        
    def get_smaller_or_equal_in_arr(self, arr, val):
        if not arr:
            return 0
            
        # find the first num > val
        start, end = 0, len(arr) - 1
        while start + 1 < end:
            mid = (start + end) // 2
            if arr[mid] > val:
                end = mid
            else:
                start = mid
        
        if arr[start] > val:
            return start
        if arr[end] > val:
            return end
        return end + 1
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)