# 单词搜索
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/word-search/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="line-height: 1.42857143;">给出一个二维的字母板和一个单词，寻找字母板网格中是否存在这个单词。</span><br></p><p>单词可以由按顺序的相邻单元的字母组成，其中相邻单元指的是水平或者垂直方向相邻。每个单元中的字母最多只能使用一次。</p>
 ### 样例说明
 **样例 1:**
```
输入：["ABCE","SFCS","ADEE"]，"ABCCED"
输出：true
解释：
[    
     A B C E
     S F C S 
     A D E E
]
(0,0)A->(0,1)B->(0,2)C->(1,2)C->(2,2)E->(2,1)D
```

**样例 2:**
```
输入：["z"]，"z"
输出：true
解释：
[ z ]
(0,0)z
```
 ### 参考代码
 Given a 2D board and a word, find if the word exists in the grid.&nbsp;<div>The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.&nbsp;</div><div><br></div><div>For example,&nbsp;</div><div>Given board =&nbsp;</div><div><br></div><div>[&nbsp;</div><div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;["ABCE"],&nbsp;</div><div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;["SFCS"],&nbsp;</div><div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;["ADEE"]&nbsp;</div><div>]&nbsp;</div><div>word = "ABCCED", -&gt; returns true,&nbsp;</div><div>word = "SEE", -&gt; returns true,&nbsp;</div><div>word = "ABCB", -&gt; returns false.</div><div><br></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博：</span><font color="#666e70" face="Open Sans, Arial, sans-serif"><span style="line-height: 22.3999996185303px;"><a href="http://weibo.com/3948019741/BsAol7c9Q" target="_blank">http://weibo.com/3948019741/BsAol7c9Q</a></span></font><br></div>
```python
class Solution:
    # @param board, a list of lists of 1 length string
    # @param word, a string
    # @return a boolean
    def exist(self, board, word):
        # write your code here
        # Boundary Condition
        if word == []:
            return True
        m = len(board)
        if m == 0:
            return False
        n = len(board[0])
        if n == 0:
            return False
        # Visited Matrix
        visited = [[False for j in range(n)] for i in range(m)]
        # DFS
        for i in range(m):
            for j in range(n):
                if self.exist2(board, word, visited, i, j):
                    return True
        return False

    def exist2(self, board, word, visited, row, col):
        if word == '':
            return True
        m, n = len(board), len(board[0])
        if row < 0 or row >= m or col < 0 or col >= n:
            return False
        if board[row][col] == word[0] and not visited[row][col]:
            visited[row][col] = True
            # row - 1, col
            if self.exist2(board, word[1:], visited, row - 1, col) or self.exist2(board, word[1:], visited, row, col - 1) or self.exist2(board, word[1:], visited, row + 1, col) or self.exist2(board, word[1:], visited, row, col + 1):
                return True
            else:
                visited[row][col] = False
        return False
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)