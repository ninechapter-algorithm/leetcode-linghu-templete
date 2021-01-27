# 和为零的子矩阵
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/submatrix-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数矩阵，请找出一个子矩阵，使得其数字之和等于0.输出答案时，请返回左上数字和右下数字的坐标。

如果有多个答案, 你可以返回其中任意一个.
 ### 样例说明
 **样例 1:**

```
输入:
[
  [1, 5, 7],
  [3, 7, -8],
  [4, -8 ,9]
]
输出: [[1, 1], [2, 2]]
```

**样例 2:**

```
输入: 
[
  [0, 1],
  [1, 0]
]
输出: [[0, 0], [0, 0]]
```
 ### 参考代码
 用前缀和优化, 令 `sum[i][j] = sum[0][j] + sum[1][j] + ... + sum[i][j]`

然后枚举上下边界, 这样就相当于在一行内, 求一个数组连续子串和为0的问题了.
```python
class Solution:
    """
    @param: matrix: an integer matrix
    @return: the coordinate of the left-up and right-down number
    """
    def submatrixSum(self, matrix):
        if not matrix or not matrix[0]:
            return None
            
        n, m = len(matrix), len(matrix[0])
        for top in range(n):
            arr = [0] * m
            for down in range(top, n):
                prefix_hash = {0: -1}
                prefix_sum = 0
                for col in range(m):
                    arr[col] += matrix[down][col]
                    prefix_sum += arr[col]
                    if prefix_sum in prefix_hash:
                        return [(top, prefix_hash[prefix_sum] + 1), (down, col)]
                    prefix_hash[prefix_sum] = col
                    
        return None
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)