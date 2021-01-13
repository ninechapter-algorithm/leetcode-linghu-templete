# 单词接龙
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/word-ladder/?utm_source=sc-github-wzz)
 ## 题目描述
 给出两个单词（*start*和*end*）和一个字典，找出从*start*到*end*的最短转换序列，输出最短序列的长度。

变换规则如下：

1. 每次只能改变一个字母。
2. 变换过程中的中间单词必须在字典中出现。(起始单词和结束单词不需要出现在字典中)
 ### 样例说明
 **样例 1:**
```
输入：start = "a"，end = "c"，dict =["a","b","c"]
输出：2
解释：
"a"->"c"
```


**样例 2:**
```
输入：start ="hit"，end = "cog"，dict =["hot","dot","dog","lot","log"]
输出：5
解释：
"hit"->"hot"->"dot"->"dog"->"cog"
```
 ### 参考代码
 使用分层遍历的BFS版本。
```python
class Solution:
    """
    @param: start: a string
    @param: end: a string
    @param: dict: a set of string
    @return: An integer
    """
    def ladderLength(self, start, end, dict):
        dict.add(end)
        queue = collections.deque([start])
        visited = set([start])
        
        distance = 0
        while queue:
            distance += 1
            for i in range(len(queue)):
                word = queue.popleft()
                if word == end:
                    return distance
                
                for next_word in self.get_next_words(word):
                    if next_word not in dict or next_word in visited:
                        continue
                    queue.append(next_word)
                    visited.add(next_word) 

        return 0
        
    # O(26 * L^2)
    # L is the length of word
    def get_next_words(self, word):
        words = []
        for i in range(len(word)):
            left, right = word[:i], word[i + 1:]
            for char in 'abcdefghijklmnopqrstuvwxyz':
                if word[i] == char:
                    continue
                words.append(left + char + right)
        return words
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)