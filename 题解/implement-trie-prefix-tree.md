# 实现 Trie（前缀树）
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/implement-trie-prefix-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个 Trie，包含 `insert`, `search`, 和 `startsWith` 这三个方法。
 ### 样例说明
 **样例 1:**

```
输入: 
  insert("lintcode")
  search("lint")
  startsWith("lint")
输出: 
  false
  true
```

**样例 2:**

```
输入:
  insert("lintcode")
  search("code")
  startsWith("lint")
  startsWith("linterror")
  insert("linterror")
  search("lintcode”)
  startsWith("linterror")
输出: 
  false
  true
  false
  true
  true
```
 ### 参考代码
 ```python
class TrieNode:
    
    def __init__(self):
        self.children = {}
        self.is_word = False
    
    
class Trie:
    
    def __init__(self):
        self.root = TrieNode()

    """
    @param: word: a word
    @return: nothing
    """
    def insert(self, word):
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        
        node.is_word = True

    """
    return the node in the trie if exists 
    """
    def find(self, word):
        node = self.root
        for c in word:
            node = node.children.get(c)
            if node is None:
                return None
        return node
        
    """
    @param: word: A string
    @return: if the word is in the trie.
    """
    def search(self, word):
        node = self.find(word)
        return node is not None and node.is_word

    """
    @param: prefix: A string
    @return: if there is any word in the trie that starts with the given prefix.
    """
    def startsWith(self, prefix):
        return self.find(prefix) is not None
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)