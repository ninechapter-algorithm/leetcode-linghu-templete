# 合并k个排序数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/merge-k-sorted-arrays/?utm_source=sc-github-wzz)
 ## 题目描述
 将 *k* 个有序数组合并为一个大的有序数组。
 ### 样例说明
 **样例 1:**

```
输入:
  [
    [1, 3, 5, 7],
    [2, 4, 6],
    [0, 8, 9, 10, 11]
  ]
输出: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
```

**样例 2:**

```
输入: 
  [
    [1,2,3],
    [1,2]
  ]
输出: [1,1,2,2,3]
```
 ### 参考代码
 使用 Heapq 的方法
最快，因为不需要创建额外空间。
时间复杂度和其他的算法一致，都是 $O(NlogK)$ N 是所有元素个数
```python
import heapq


class Solution:
    """
    @param arrays: k sorted integer arrays
    @return: a sorted array
    """
    def mergekSortedArrays(self, arrays):
        result = []
        heap = []
        for index, array in enumerate(arrays):
            if len(array) == 0:
                continue
            heapq.heappush(heap, (array[0], index, 0))
             
        while len(heap):
            val, x, y = heap[0]
            heapq.heappop(heap)
            result.append(val)
            if y + 1 < len(arrays[x]):
                heapq.heappush(heap, (arrays[x][y + 1], x, y + 1))
            
        return result
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)