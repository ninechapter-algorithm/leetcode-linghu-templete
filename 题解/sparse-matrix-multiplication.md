# 稀疏矩阵乘法
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sparse-matrix-multiplication/?utm_source=sc-github-wzz)
 ## 题目描述
 给定两个 [稀疏矩阵](https://en.wikipedia.org/wiki/Sparse_matrix) A 和 B，返回AB的结果。
您可以假设A的列数等于B的行数。
 ### 样例说明
 **样例1**
```
输入：
[[1,0,0],[-1,0,3]]
[[7,0,0],[0,0,0],[0,0,1]]
输出：
[[7,0,0],[-7,0,3]]
解释：
A = [
  [ 1, 0, 0],
  [-1, 0, 3]
]

B = [
  [ 7, 0, 0 ],
  [ 0, 0, 0 ],
  [ 0, 0, 1 ]
]


     |  1 0 0 |   | 7 0 0 |   |  7 0 0 |
AB = | -1 0 3 | x | 0 0 0 | = | -7 0 3 |
                  | 0 0 1 |
```
**样例2**
```
输入：
[[1,0],[0,1]]
[[0,1],[1,0]]
输出：
[[0,1],[1,0]]
```
 ### 参考代码
 一种时间复杂度也为 $O(k * n^2)$ 的办法（k 为一行中的非零位个数）
这种办法比较巧妙，通过初始化结果矩阵，然后把非零位逐个累乘累加的办法，而不是按照原来的矩阵乘法顺序在做。
```python
class Solution:
    """
    @param A: a sparse matrix
    @param B: a sparse matrix
    @return: the result of A * B
    """
    def multiply(self, A, B):
        n = len(A)
        m = len(A[0])
        k = len(B[0])

        C = [[0] * k for i in range(n)]

        for i in range(n):
            for j in range(m):
                if A[i][j] != 0:
                    for l in range(k):
                        C[i][l] += A[i][j] * B[j][l]
        return C
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)