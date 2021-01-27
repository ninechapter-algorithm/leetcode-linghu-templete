# 字符串解码
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/decode-string/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个表达式 `s`，此表达式包括数字，字母以及方括号。在方括号前的数字表示方括号内容的重复次数(括号内的内容可以是字符串或另一个表达式)，请将这个表达式展开成一个字符串。
 ### 样例说明
 **样例1**

```
输入: S = abc3[a]
输出: "abcaaa"
```

**样例2**

```
输入: S = 3[2[ad]3[pf]]xyz
输出: "adadpfpfpfadadpfpfpfadadpfpfpfxyz"
```

 ### 参考代码
 把所有字符一个个放到 stack 里， 如果碰到了 `]`，就从 stack 找到对应的字符串和重复次数，decode 之后再放回 stack 里
```python
class Solution:
    """
    @param s: an expression includes numbers, letters and brackets
    @return: a string
    """
    def expressionExpand(self, s):
        stack = []
        for c in s:
            if c != ']':
                stack.append(c)
                continue
                
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
        
        return ''.join(stack)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)