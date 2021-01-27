# 摆动排序 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/wiggle-sort-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个数组`nums`，将它重排列如下形式
```
nums[0] < nums[1] > nums[2] < nums[3]....
```
 ### 样例说明
 
 ### 参考代码
 $O(n)$ 的时间，$O(1)$ 额外空间
算法一言难尽，去上九章算法强化班吧。

这个问题的做法是，先找到中位数，然后根据中位数把数组分成三个部分，< median, == median, > median
然后把这三个部分按照从大到小摆放在从右到左每次跳一格的位置。
```python
class Solution:
    """
    @param: nums: A list of integers
    @return: nothing
    """
    def wiggleSort(self, nums):
        if not nums:
            return
        
        # partition nums into smaller half and bigger half
        # all nums in smaller half <= any num in bigger half
        median = self.find_median(nums)
        
        n = len(nums)

        # reorder the nums from
        # 0 => n-1(odd), (n-2)(even)
        # 1 => n-3
        # 2 => n-5
        # ...
        # (n - 1) / 2 => 0
        # (n - 1) / 2 + 1 => n - 2(odd), n - 1(even)
        # (n - 1) / 2 + 2 => n - 4(odd), n - 3(even)
        # ... 
        def get_index(i):
            if i <= (n - 1) // 2:
                return n - i * 2 - 1 - (n + 1) % 2
            i -= (n - 1) // 2 + 1
            return n - i * 2 - 1 - n % 2
            
        # 3-way partition
        left, i, right = 0, 0, n - 1
        while i <= right:
            if nums[get_index(i)] < median:
                nums[get_index(left)], nums[get_index(i)] = nums[get_index(i)], nums[get_index(left)]
                i += 1
                left += 1
            elif nums[get_index(i)] == median:
                i += 1
            else:
                nums[get_index(right)], nums[get_index(i)] = nums[get_index(i)], nums[get_index(right)]
                right -= 1
        
    def find_median(self, nums):
        return self.find_kth(nums, 0, len(nums) - 1, (len(nums) - 1) // 2)
    
    def find_kth(self, nums, start, end, kth):
        # k is zero based
        left, right = start, end
        mid = nums[(left + right) // 2]
        
        while left <= right:
            while left <= right and nums[left] < mid:
                left += 1
            while left <= right and nums[right] > mid:
                right -= 1
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left, right = left + 1, right - 1
                
        if kth <= right:
            return self.find_kth(nums, start, right, kth)
        elif kth >= left:
            return self.find_kth(nums, left, end, kth)
        else:
            return nums[kth]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)