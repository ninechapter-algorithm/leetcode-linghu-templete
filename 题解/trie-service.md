# 查找树服务
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/trie-service/?utm_source=sc-github-wzz)
 ## 题目描述
 通过<字符串，值\>的集合来建立树结构，每个结点保存前10大的数值。
 ### 样例说明
 **样例1**

```
输入:  
 <"abc", 2>
 <"ac", 4>
 <"ab", 9>
输出:<a[9,4,2]<b[9,2]<c[2]<>>c[4]<>>> 
解释:
			Root
             / 
           a(9,4,2)
          /    \
        b(9,2) c(4)
       /
     c(2)
```

**样例2**

```
输入:  
<"a", 10>
<"c", 41>
<"b", 50>
<"abc", 5>
输出: <a[10,5]<b[5]<c[5]<>>>b[50]<>c[41]<>>
```
 ### 参考代码
 先遍历一遍数，然后重构树进行求解
```python
"""
Definition of TrieNode:
class TrieNode:
    def __init__(self):
        # <key, value>: <Character, TrieNode>
        self.children = collections.OrderedDict()
        self.top10 = []
"""
class TrieService:

    def __init__(self):
        self.root = TrieNode()

    def get_root(self):
        # Return root of trie root, and 
        # lintcode will print the tree struct.
        return self.root

    # @param {str} word a string
    # @param {int} frequency an integer
    # @return nothing
    def insert(self, word, frequency):
        # Write your your code here
        node = self.root
        for letter in word:
            child = node.children.get(letter, None)

            if child is None:
                child = TrieNode()

            node.children[letter] = child
            self.add_frequency(child.top10, frequency)

            node = child

    def add_frequency(self, top10, frequency):
        top10.append(frequency)
        index = len(top10) - 1
        while index > 0:
            if top10[index] > top10[index - 1]:
                top10[index], top10[index - 1] = top10[index - 1], top10[index]
                index -= 1
            else:
                break
        if len(top10) > 10:
            top10.pop()
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)