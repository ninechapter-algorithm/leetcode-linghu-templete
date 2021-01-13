# Letter Combinations of a Phone Number II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/letter-combinations-of-a-phone-number-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给一些不包含`0`和`1`的数字字符串和一个字典，对于每个数字字符串，每个数字代表一个字母，请返回字典中可以匹配的字母组合的数量。

如果可以用一个数字字符串可以表示出一个单词的前缀，我们认为他们之间是匹配的。

下图的手机按键图，就表示了每个数字可以代表的字母。

1|2<br />ABC|3<br />DEF
:--:|:--:|:--:
**4**<br />**GHI**|**5**<br />**JKL**|**6**<br />**MNO**
**7**<br />**PQRS**|**8**<br />**TUV**|**9**<br />**WXYZ**
 ### 样例说明
 
 ### 参考代码
 这个题不需要 DFS，只需要建 Trie 就行。
存在 Trie 里的不是单词，而是单词转成数字之后的字符串。
比如词典里有 `["a", "abc", "de", "fg"]`，存在 Trie 里的就是 `["2", "222", "33", "34"]`
之后的话 for queries 里的每个 query，在 Trie 里沿着 query 走到对应的节点上看一下计数就行。

```
[[python]]
REVERSE_KEYBOARD = {
    "a": "2", "b": "2", "c": "2",
    "d": "3", "e": "3", "f": "3",
    "g": "4", "h": "4", "i": "4",
    "j": "5", "k": "5", "l": "5",
    "m": "6", "n": "6", "o": "6",
    "p": "7", "q": "7", "r": "7", "s": "7",
    "t": "8", "u": "8", "v": "8",
    "w": "9", "x": "9", "y": "9", "z": "9",
}

class TrieNode:
    
    def __init__(self):
        self.word_count = 0
        self.children = {}
        
    def add(self, word):
        node = self
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
            node.word_count += 1
    
    
class Solution:
    """
    @param queries: the queries
    @param dict: the words
    @return: return the queries' answer
    """
    def letterCombinationsII(self, queries, dict):
        root = TrieNode()
        for word in dict:
            digit_word = ''.join([
                REVERSE_KEYBOARD[c]
                for c in word
            ])
            root.add(digit_word)
            
        results = []
        for query in queries:
            node = root
            for char in query:
                if char not in node.children:
                    node = None
                    break
                node = node.children[char]
            results.append(node.word_count if node else 0)
            
        return results
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)