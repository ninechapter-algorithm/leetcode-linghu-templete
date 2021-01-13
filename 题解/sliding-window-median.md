# 滑动窗口的中位数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sliding-window-median/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个包含 n 个整数的数组，和一个大小为 *k* 的滑动窗口,从左到右在数组中滑动这个窗口，找到数组中每个窗口内的中位数。(如果数组个数是偶数，则在该窗口排序数字后，返回第 N/2 个数字。)
 ### 样例说明
 **样例 1:**
```
输入:
[1,2,7,8,5]
3
输出:
[2,7,7]

解释:
最初，窗口的数组是这样的：`[ | 1,2,7 | ,8,5]` , 返回中位数 `2`;
接着，窗口继续向前滑动一次。`[1, | 2,7,8 | ,5]`, 返回中位数 `7`;
接着，窗口继续向前滑动一次。`[1,2, | 7,8,5 | ]`, 返回中位数 `7`;
```

**样例 2:**
```
输入:
[1,2,3,4,5,6,7]
4
输出:
[2,3,4,5]

解释:
最初，窗口数组是这样的：`[ | 1,2,3,4, | 5,6,7]` , 返回中位数 `2`;
接着，窗口向前滑动一次.`[1,| 2,3,4,5 | 6,7]`,返回中位数 `3`;
接着，窗口向前滑动一次.`[1,2, | 3,4,5,6 | 7 ]`, 返回中位数 `4`;
接着，窗口向前滑动一次`[1,2,3,| 4,5,6,7 ]`, 返回中位数 `5`;
```
 ### 参考代码
 使用九章算法强化班中讲到的 HashHeap。即一个 Hash + Heap。
Hash 的 key 是 Heap 里的每个元素，值是这个元素在 Heap 中的下标。

要做这个题首先需要先做一下 Data Stream Median。这个题是只在一个集合中增加数，不删除数，然后不断的求中点。
Sliding Window Median，就是不断的增加数，删除数，然后求中点。比 Data Stream Median 难的地方就在于如何支持删除数。

因为 Data Stream Median 的方法是用 两个 Heap，一个 max heap，一个min heap。所以删除的话，就需要让 heap 也支持删除操作。
由于 Python 的 heapq 并不支持 logn 时间内的删除操作，因此只能自己实现一个 hash + heap 的方法。

总体时间复杂度 $O(nlogk)$，n是元素个数，k 是 window 的大小。
```python
class HashHeap:
    
    def __init__(self, desc=False):
        self.hash = dict()
        self.heap = []
        self.desc = desc
        
    @property
    def size(self):
        return len(self.heap)
        
    def push(self, item):
        self.heap.append(item)
        self.hash[item] = self.size - 1
        self._sift_up(self.size - 1)
        
    def pop(self):
        item = self.heap[0]
        self.remove(item)
        return item
    
    def top(self):
        return self.heap[0]
        
    def remove(self, item):
        if item not in self.hash:
            return
            
        index = self.hash[item]
        self._swap(index, self.size - 1)
        
        del self.hash[item]
        self.heap.pop()
        
        # in case of the removed item is the last item
        if index < self.size:
            self._sift_up(index)
            self._sift_down(index)

    def _smaller(self, left, right):
        return right < left if self.desc else left < right

    def _sift_up(self, index):
        while index != 0:
            parent = index // 2
            if self._smaller(self.heap[parent], self.heap[index]):
                break
            self._swap(parent, index)
            index = parent
    
    def _sift_down(self, index):
        if index is None:
            return
        while index * 2 < self.size:
            smallest = index
            left = index * 2
            right = index * 2 + 1
            
            if self._smaller(self.heap[left], self.heap[smallest]):
                smallest = left
                
            if right < self.size and self._smaller(self.heap[right], self.heap[smallest]):
                smallest = right
                
            if smallest == index:
                break
            
            self._swap(index, smallest)
            index = smallest
        
    def _swap(self, i, j):
        elem1 = self.heap[i]
        elem2 = self.heap[j]
        self.heap[i] = elem2
        self.heap[j] = elem1
        self.hash[elem1] = j
        self.hash[elem2] = i
    
class Solution:
    """
    @param nums: A list of integers
    @param k: An integer
    @return: The median of the element inside the window at each moving
    """
    def medianSlidingWindow(self, nums, k):
        if not nums or len(nums) < k:
            return []
            
        self.maxheap = HashHeap(desc=True)
        self.minheap = HashHeap()
        
        for i in range(0, k - 1):
            self.add((nums[i], i))
            
        medians = []
        for i in range(k - 1, len(nums)):
            self.add((nums[i], i))
            # print(self.maxheap.heap, self.median, self.minheap.heap)
            medians.append(self.median)
            self.remove((nums[i - k + 1], i - k + 1))
            # print(self.maxheap.heap, self.median, self.minheap.heap)
            
        return medians
            
    def add(self, item):
        if self.maxheap.size > self.minheap.size:
            self.minheap.push(item)
        else:
            self.maxheap.push(item)
            
        if self.maxheap.size == 0 or self.minheap.size == 0:
            return
            
        if self.maxheap.top() > self.minheap.top():
            self.maxheap.push(self.minheap.pop())
            self.minheap.push(self.maxheap.pop())
        
    def remove(self, item):
        self.maxheap.remove(item)
        self.minheap.remove(item)
        if self.maxheap.size < self.minheap.size:
            self.maxheap.push(self.minheap.pop())
        
    @property
    def median(self):
        return self.maxheap.top()[0]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)