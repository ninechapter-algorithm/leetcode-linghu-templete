# 单词搜索 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/word-search-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出一个由小写字母组成的矩阵和一个字典。找出所有同时在字典和矩阵中出现的单词。一个单词可以从矩阵中的任意位置开始，可以向左/右/上/下四个相邻方向移动。一个字母在一个单词中只能被使用一次。且字典中不存在重复单词</p>
 ### 样例说明
 **样例 1:**
```
输入：["doaf","agai","dcan"]，["dog","dad","dgdg","can","again"]
输出：["again","can","dad","dog"]
解释：
  d o a f
  a g a i
  d c a n
矩阵中查找，返回 ["again","can","dad","dog"]。
```

**样例 2:**
```
输入：["a"]，["b"]
输出：[]
解释：
 a
矩阵中查找，返回 []。
```
 ### 参考代码
 不用 Trie，直接使用哈希表的方法
```python
DIRECTIONS = [(0, -1), (0, 1), (-1, 0), (1, 0)]

class Solution:
    """
    @param board: A list of lists of character
    @param words: A list of string
    @return: A list of string
    """
    def wordSearchII(self, board, words):
        if board is None or len(board) == 0:
            return []
        
        # pre-process
        # 预处理
        word_set = set(words)
        prefix_set = set()
        for word in words:
            for i in range(len(word)):
                prefix_set.add(word[:i + 1])
        
        result = set()
        for i in range(len(board)):
            for j in range(len(board[0])):
                c = board[i][j]
                self.search(
                    board,
                    i,
                    j,
                    board[i][j],
                    word_set,
                    prefix_set,
                    set([(i, j)]),
                    result,
                )
                
        return list(result)
        
    def search(self, board, x, y, word, word_set, prefix_set, visited, result):
        if word not in prefix_set:
            return
        
        if word in word_set:
            result.add(word)
        
        for delta_x, delta_y in DIRECTIONS:
            x_ = x + delta_x
            y_ = y + delta_y
            
            if not self.inside(board, x_, y_):
                continue
            if (x_, y_) in visited:
                continue
            
            visited.add((x_, y_))
            self.search(
                board,
                x_,
                y_,
                word + board[x_][y_],
                word_set,
                prefix_set,
                visited,
                result,
            )
            visited.remove((x_, y_))
            
    def inside(self, board, x, y):
        return 0 <= x < len(board) and 0 <= y < len(board[0])
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)