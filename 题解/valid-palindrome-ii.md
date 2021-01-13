# 有效回文 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/valid-palindrome-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个非空字符串 `s`，你最多可以删除一个字符。判断是否可以把它变成回文串。
 ### 样例说明
 **样例 1:**

```
输入: s = "aba"
输出: true
解释: 原本就是回文串
```

**样例 2:**

```
输入: s = "abca"
输出: true
解释: 删除 'b' 或 'c'
```

**样例 3:**

```
输入: s = "abc"
输出: false
解释: 删除任何一个字符都不能使之变成回文串
```
 ### 参考代码
 双指针算法。从两头走到中间，发现第一对不一样的字符之后，要么删左边的，要么删右边的。
```python
class Solution:
    """
    @param s: a string
    @return: nothing
    """
    def validPalindrome(self, s):
        left, right = self.twoPointer(s, 0, len(s) - 1)            
        if left >= right:
            return True
            
        return self.isPalindrome(s, left + 1, right) or self.isPalindrome(s, left, right - 1)

    def isPalindrome(self, s, left, right):
        left, right = self.twoPointer(s, left, right)
        return left >= right
        
    def twoPointer(self, s, left, right):
        while left < right:
            if s[left] != s[right]:
                return left, right
            left += 1
            right -= 1
        return left, right
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)