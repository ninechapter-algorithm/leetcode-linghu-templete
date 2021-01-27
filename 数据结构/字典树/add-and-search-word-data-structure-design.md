# 单词的添加与查找
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/add-and-search-word-data-structure-design/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一个包含下面两个操作的数据结构：`addWord(word)`, `search(word)`

`addWord(word)`会在数据结构中添加一个单词。而`search(word)`则支持普通的单词查询或是只包含`.`和`a-z`的简易正则表达式的查询。

一个 `.` 可以代表一个任何的字母。
 ### 样例说明
 **样例 1:**

```
输入:
  addWord("a")
  search(".")
输出: 
  true
```

**样例 2:**

```
输入: 
  addWord("bad")
  addWord("dad")
  addWord("mad")
  search("pad")  
  search("bad")  
  search(".ad")  
  search("b..") 
输出:
  false
  true
  true
  true 
```
 ### 参考代码
 ```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_word = False


class WordDictionary:
    
    def __init__(self):
        self.root = TrieNode()
        
    """
    @param: word: Adds a word into the data structure.
    @return: nothing
    """
    def addWord(self, word):
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.is_word =True

    """
    @param: word: A word could contain the dot character '.' to represent any one letter.
    @return: if the word is in the data structure.
    """
    def search(self, word):
        if word is None:
            return False
        return self.search_helper(self.root, word, 0)
        
    def search_helper(self, node, word, index):
        if node is None:
            return False
            
        if index >= len(word):
            return node.is_word
        
        char = word[index]
        if char != '.':
            return self.search_helper(node.children.get(char), word, index + 1)
            
        for child in node.children:
            if self.search_helper(node.children[child], word, index + 1):
                return True
                
        return False
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)