# 被围绕的区域
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/surrounded-regions/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个二维的矩阵，包含 `'X'` 和 `'O'`, 找到所有被 `'X'` 围绕的区域，并用 `'X'` 替换其中所有的 `'O'`。

 ### 样例说明
 **样例 1:**

```
输入:
  X X X X
  X O O X
  X X O X
  X O X X
输出: 
  X X X X
  X X X X
  X X X X
  X O X X
```

**样例 2:**

```
输入: 
  X X X X
  X O O X
  X O O X
  X O X X
输出: 
  X X X X
  X O O X
  X O O X
  X O X X
```
 ### 参考代码
 高频题班的版本，使用 BFS 的方法
先把从边界开始的 O 都标记为 W，这样非 W 的地方就全都需要标记为 X
```python
// version: 高频题班
class Solution:
    # @param {list[list[str]]} board a 2D board containing 'X' and 'O'
    # @return nothing 
    def surroundedRegions(self, board):
        # Write your code here
        if not any(board):
            return

        n, m = len(board), len(board[0])
        q = [ij for k in range(max(n,m)) for ij in ((0, k), (n-1, k), (k, 0), (k, m-1))]
        while q:
            i, j = q.pop()
            if 0 <= i < n and 0 <= j < m and board[i][j] == 'O':
                board[i][j] = 'W'
                q += (i, j-1), (i, j+1), (i-1, j), (i+1, j)

        board[:] = [['XO'[c == 'W'] for c in row] for row in board]
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)