# 字模式 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/word-pattern-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个`pattern`和一个字符串`str`，查找`str`是否遵循相同的模式。
这里**遵循**的意思是一个完整的匹配，在一个字母的`模式`和一个**非空的**单词`str`之间有一个[双向连接](https://baike.baidu.com/item/%E5%8F%8C%E5%B0%84/942799?fr=aladdin "bijection")的模式对应。(如果`a`对应`s`，那么`b`不对应`s`。例如，给定的模式= `"ab"`， str = `"ss"`，返回`false`）。
 ### 样例说明
 **样例1**

```plain
输入:
pattern = "abab"
str = "redblueredblue"
输出: true
说明: "a"->"red","b"->"blue"
```

**样例2**

```plain
输入:
pattern = "aaaa"
str = "asdasdasdasd"
输出: true
说明: "a"->"asd"
```

**样例3**

```plain
输入:
pattern = "aabb"
str = "xyzabcxzyabc"
输出: false
```


 ### 参考代码
 用九章算法班中讲过的深度优先搜索算法。
这个题不能使用动态规划或者记忆化搜索，因为参数列表中 mapping 和 used 无法记录到记忆化的哈希表中。
```python
class Solution:
    """
    @param pattern: a string,denote pattern string
    @param str: a string, denote matching string
    @return: a boolean
    """
    def wordPatternMatch(self, pattern, string):
        return self.is_match(pattern, string, {}, set())

    def is_match(self, pattern, string, mapping, used):
        if not pattern:
            return not string
            
        char = pattern[0]
        if char in mapping:
            word = mapping[char]
            if not string.startswith(word):
                return False
            return self.is_match(pattern[1:], string[len(word):], mapping, used)
            
        for i in range(len(string)):
            word = string[:i + 1]
            if word in used:
                continue
            
            used.add(word)
            mapping[char] = word
            
            if self.is_match(pattern[1:], string[i + 1:], mapping, used):
                return True
            
            del mapping[char]
            used.remove(word)
            
        return False
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)