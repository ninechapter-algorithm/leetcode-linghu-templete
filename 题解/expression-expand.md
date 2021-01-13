# 字符串解码
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/expression-expand/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个表达式 `s`，此表达式包括数字，字母以及方括号。在方括号前的数字表示方括号内容的重复次数(括号内的内容可以是字符串或另一个表达式)，请将这个表达式展开成一个字符串。
 ### 样例说明
 
 ### 参考代码
 把所有字符一个个放到 stack 里，当碰到 "]" 的时候，就从 stack 把对应的字符串和重复次数找到，展开，然后再丢回 stack 里，
```python
class Solution:
    """
    @param s: an expression includes numbers, letters and brackets
    @return: a string
    """
    def expressionExpand(self, s):
        stack = []
        for c in s:
            if c == ']':
                strs = []
                while stack and stack[-1] != '[':
                    strs.append(stack.pop())
                
                # skip '['
                stack.pop()
                
                repeats = 0
                base = 1
                while stack and stack[-1].isdigit():
                    repeats += (ord(stack.pop()) - ord('0')) * base
                    base *= 10
                stack.append(''.join(reversed(strs)) * repeats)
            else:
                stack.append(c)
        
        return ''.join(stack)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)