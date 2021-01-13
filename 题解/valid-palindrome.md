# 有效回文串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/valid-palindrome/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串，判断其是否为一个回文串。只考虑字母和数字，忽略大小写。
 ### 样例说明
 **样例 1:**

```
输入: "A man, a plan, a canal: Panama"
输出: true
解释: "amanaplanacanalpanama"
```

**样例 2:**

```
输入: "race a car"
输出: false
解释: "raceacar"
```
 ### 参考代码
 使用两根指针遍历整个字符串即可.

假定有指针i, j, 其中i是从前往后遍历, j是从后往前遍历.

当i在j左边时继续循环, 每一次将i右移到数字/字母上, j左移到数字/字母上, 

比较二者对应的字符串内的字符是否相同, 不相同则原字符串不是回文串. 

如果全部的比较都相同, 说明是回文串.
```python
class Solution:
    # @param {string} s A string
    # @return {boolean} Whether the string is a valid palindrome
    def isPalindrome(self, s):
        start, end = 0, len(s) - 1
        while start < end:
            while start < end and not s[start].isalpha() and not s[start].isdigit():
                start += 1
            while start < end and not s[end].isalpha() and not s[end].isdigit():
                end -= 1
            if start < end and s[start].lower() != s[end].lower():
                return False
            start += 1
            end -= 1
        return True
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)