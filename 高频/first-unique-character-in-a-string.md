# 第一个只出现一次的字符
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/first-unique-character-in-a-string/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个字符串，找出第一个只出现一次的字符。
 ### 样例说明
 ```
样例 1:
	输入: "abaccdeff"
	输出:  'b'
	
	解释:
	'b' 是第一个出现一次的字符


样例 2:
	输入: "aabccd"
	输出:  'b'
	
	解释:
	'b' 是第一个出现一次的字符


```
 ### 参考代码
 辅助数组记录字符出现次数。
```python
class Solution:
    """
    @param str: str: the given string
    @return: char: the first unique character in a given string
    """
    def firstUniqChar(self, str):
        counter = {}

        for c in str:
            counter[c] = counter.get(c, 0) + 1

        for c in str:
            if counter[c] == 1:
                return c
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)