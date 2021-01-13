# 丑数 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/ugly-number-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一个算法，找出只含素因子`2`，`3`，`5` 的第 *n* 小的数。

符合条件的数如：`1, 2, 3, 4, 5, 6, 8, 9, 10, 12...`

 ### 样例说明
 **样例 1：**
```
输入：9
输出：10
```
**样例 2：**
```
输入：1
输出：1
```
 ### 参考代码
 使用九章算法班中讲的 heap
时间复杂度 $O(nlogn)$
```python
import heapq

class Solution:
    """
    @param {int} n an integer.
    @return {int} the nth prime number as description.
    """
    def nthUglyNumber(self, n):
        heap = [1]
        visited = set([1])
        
        val = None
        for i in range(n):
            val = heapq.heappop(heap)
            for factor in [2, 3, 5]:
                if val * factor not in visited:
                    visited.add(val * factor)
                    heapq.heappush(heap, val * factor)
            
        return val
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)