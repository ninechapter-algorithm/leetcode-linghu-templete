# 将表达式转换为逆波兰表达式
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/convert-expression-to-reverse-polish-notation/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串数组，它代表一个表达式，返回该表达式的逆波兰表达式。（去掉括号）
 ### 样例说明
 **样例 1:**

```
输入: ["3", "-", "4", "+", "5"]
输出: ["3", "4", "-", "5", "+"]
解释: 3 - 4 + 5 = -1 + 5 = 4
    3 4 - 5 + = -1 5 + = 4
```

**样例 2:**

```
输入: ["(", "5", "-", "6", ")", "*", "7"]
输出: ["5","6","-","7","*"]
解释: (5 - 6) * 7 = -1 * 7 = -7
    5 6 - 7 * = -1 7 * = -7
```
 ### 参考代码
 借助 **栈** 我们可以实现中缀表达式到后缀表达式(即逆波兰表达式, RPN)的转换.

从左到右遍历中缀表达式:

1. 如果碰到 **数字**, 直接追加到 RPN 末尾.
2. 如果碰到 **左括号**, 入栈
3. 如果碰到 **右括号**, 弹栈, 并将弹出的元素依次追加到 RPN 末尾, 直至左括号弹出(左括号不追加至PN)
4. 如果碰到 **运算符**, 弹栈直至栈顶元素优先级 **小于** 当前运算符, 所有弹出的元素依次追加到 RPN 末尾, 最后再将该运算符入栈

出于方便, 我们设定所有元素的优先级: `*/` 最高, `+-` 次之, 然后是数字, 最后是括号.

(把括号设为最低是因为, 碰到运算符弹栈时, 遇到括号也要停止, 所以可以直接设为最低)

最后, 如果栈还有剩余, 弹栈, 依次追加到 RPN 末尾, 然后我们就得到了正确结果 RPN.
```python
class Solution:
    """
    @param expression: A string array
    @return: The Reverse Polish notation of this expression
    """
    def convertToRPN(self, expression):
        stk = []
        RPN = []
        for s in expression:
            if s == '(':
                stk.append(s)
            elif s == ')':
                pos = stk[::-1].index('(')
                RPN += stk[::-1][:pos]
                stk = stk[:-pos-1]
            elif s[0] in '1234567890':
                RPN.append(s)
            else:
                priority = self.getPriority(s)
                while len(stk) and self.getPriority(stk[-1]) >= priority:
                    RPN.append(stk[-1])
                    stk.pop()
                stk.append(s)
        RPN += stk[::-1]
        return RPN
    
    def getPriority(self, s):
        if s in '*/':
            return 3 
        if s in '+-':
            return 2 
        if s in '()':
            return 1 
        return 0
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)