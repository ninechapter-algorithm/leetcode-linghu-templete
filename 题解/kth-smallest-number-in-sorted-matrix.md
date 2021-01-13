# 排序矩阵中的从小到大第k个数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/kth-smallest-number-in-sorted-matrix/?utm_source=sc-github-wzz)
 ## 题目描述
 在一个排序矩阵中找从小到大的第 *k* 个整数。

排序矩阵的定义为：每一行递增，每一列也递增。
 ### 样例说明
 **样例 1:**

```
输入:
[
  [1 ,5 ,7],
  [3 ,7 ,8],
  [4 ,8 ,9],
]
k = 4
输出: 5
```

**样例 2:**

```
输入: 
[
  [1, 2],
  [3, 4]
]
k = 3
输出: 3
```
 ### 参考代码
 使用 heapq
注意 visited 不能开成一个二维数组，因为那样会增加时间复杂度。比如 K=1 的时候，理应 O(1) 的时间返回。开一个二维数组的耗费显然不只是 O(1) 的
```python
import heapq

class Solution:
    """
    @param matrix: a matrix of integers
    @param k: An integer
    @return: the kth smallest number in the matrix
    """
    def kthSmallest(self, matrix, k):
        n = len(matrix)
        if n == 0:
            return None
        
        m = len(matrix[0])
        if m == 0:
            return None
            
        minheap = [(matrix[0][0], 0, 0)]
        visited = set([0])
        num = None
        for _ in range(k):
            num, x, y = heapq.heappop(minheap)
            if x + 1 < n and (x + 1) * m + y not in visited:
                heapq.heappush(minheap, (matrix[x + 1][y], x + 1, y))
                visited.add((x + 1) * m + y)
            if y + 1 < m and x * m + y + 1 not in visited:
                heapq.heappush(minheap, (matrix[x][y + 1], x, y + 1))
                visited.add(x * m + y + 1)

        return num
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)