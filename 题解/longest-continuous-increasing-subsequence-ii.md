# 最长上升连续子序列 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-continuous-increasing-subsequence-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数矩阵. 找出矩阵中的最长连续上升子序列, 返回它的长度.

最长连续上升子序列可以从任意位置开始, 向上/下/左/右移动.
 ### 样例说明
 **样例 1:**

```
输入: 
    [
      [1, 2, 3, 4, 5],
      [16,17,24,23,6],
      [15,18,25,22,7],
      [14,19,20,21,8],
      [13,12,11,10,9]
    ]
输出: 25
解释: 1 -> 2 -> 3 -> 4 -> 5 -> ... -> 25 (由外向内螺旋)
```

**样例 2:**

```
输入: 
    [
      [1, 2],
      [5, 3]
    ]
输出: 5
解释: 1 -> 2 -> 3 -> 5
```
 ### 参考代码
 使用九章算法强化班，动态规划专题班中讲过的 **序列性动态规划**

我们把二维矩阵打散成为一位数组，数组中每个元素记录二维矩阵中的坐标和高度。
然后把一位数组按照高度排序。

f[i] 表示第 i 个点结束的最长序列，得到公式：
```
f[i] = max{f[j] + 1 |  j < i && j 这个点比 i 要低，且i和j两个点相邻}
```

最后在 max(f[i]) 就是我们要的结果。

类似的题还有 longest increasing subsequence.
```python
class Solution:
    """
    @param A: An integer matrix
    @return: an integer
    """
    def longestContinuousIncreasingSubsequence2(self, A):
        if not A or not A[0]:
            return 0
            
        n, m = len(A), len(A[0])
        points = []
        for i in range(n):
            for j in range(m):
                points.append((A[i][j], i, j))
                
        points.sort()
        
        longest_hash = {}
        for i in range(len(points)):
            key = (points[i][1], points[i][2])
            longest_hash[key] = 1
            for dx, dy in [(1, 0), (0, -1), (-1, 0), (0, 1)]:
                x, y = points[i][1] + dx, points[i][2] + dy
                if x < 0 or x >= n or y < 0 or y >= m:
                    continue
                if (x, y) in longest_hash and A[x][y] < points[i][0]:
                    longest_hash[key] = max(longest_hash[key], longest_hash[(x, y)] + 1)
                    
        return max(longest_hash.values())
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)