# 乱序字符串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/anagrams/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出一个字符串数组S，找到其中所有的乱序字符串(Anagram)。如果一个字符串是乱序字符串，那么他存在一个字母集合相同，但顺序不同的字符串也在S中。</p>
 ### 样例说明
 **样例1:**
```
输入:["lint", "intl", "inlt", "code"]
输出:["lint", "inlt", "intl"]
```

**样例 2:**
```
输入:["ab", "ba", "cd", "dc", "e"]
输出: ["ab", "ba", "cd", "dc"]
```
 ### 参考代码
 Given an array of strings, return all groups of strings that are anagrams.

Note: All inputs will be in lower-case
```python
class Solution:
    # @param strs: A list of strings
    # @return: A list of strings
    def anagrams(self, strs):
        # write your code here
        dict = {}
        for word in strs:
            sortedword = ''.join(sorted(word))
            dict[sortedword] = [word] if sortedword not in dict else dict[sortedword] + [word]
        res = []
        for item in dict:
            if len(dict[item]) >= 2:
                res += dict[item]
        return res

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)