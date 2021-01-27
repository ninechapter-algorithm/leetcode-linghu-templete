# 数据流中位数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-median-from-data-stream/?utm_source=sc-github-wzz)
 ## 题目描述
 数字是不断进入数组的，在每次添加一个新的数进入数组的同时返回当前新数组的中位数。
 ### 样例说明
 **样例1**

```plain
输入: [1,2,3,4,5]
输出: [1,1,2,2,3]
样例说明：
[1] 和 [1,2] 的中位数是 1.
[1,2,3] 和 [1,2,3,4] 的中位数是 2.
[1,2,3,4,5] 的中位数是 3.
```

**样例2**

```plain
输入: [4,5,1,3,2,6,0]
输出: [4,4,4,3,3,3,3]
样例说明：
[4], [4,5] 和 [4,5,1] 的中位数是 4.
[4,5,1,3], [4,5,1,3,2], [4,5,1,3,2,6] 和 [4,5,1,3,2,6,0] 的中位数是 3.
```


 ### 参考代码
 把比 median 小的放在 maxheap 里，把比 median 大的放在 minheap 里。median 单独放在一个变量里。
每次新增一个数的时候，先根据比当前的 median 大还是小丢到对应的 heap 里。
丢完以后，再处理左右两边的平衡性:

如果左边太少了，就把 median 丢到左边，从右边拿一个最小的出来作为 median。
如果右边太少了，就把 median 丢到右边，从左边拿一个最大的出来作为新的 median。
```python
import heapq


class Solution:
    """
    @param nums: A list of integers
    @return: the median of numbers
    """
    def medianII(self, nums):
        if not nums:
            return []
            
        self.median = nums[0]
        self.maxheap = []
        self.minheap = []
        
        medians = [nums[0]]
        for num in nums[1:]:
            self.add(num)
            medians.append(self.median)
            
        return medians

    def add(self, num):
        if num < self.median:
            heapq.heappush(self.maxheap, -num)
        else:
            heapq.heappush(self.minheap, num)
            
        # balanace
        if len(self.maxheap) > len(self.minheap):
            heapq.heappush(self.minheap, self.median)
            self.median = -heapq.heappop(self.maxheap)
        elif len(self.maxheap) + 1 < len(self.minheap):
            heapq.heappush(self.maxheap, -self.median)
            self.median = heapq.heappop(self.minheap)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)