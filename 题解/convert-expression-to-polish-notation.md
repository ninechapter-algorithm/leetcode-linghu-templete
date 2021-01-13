# 将表达式转换为波兰表达式
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/convert-expression-to-polish-notation/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串数组，它代表一个表达式，返回该表达式的波兰表达式。（去掉括号）
 ### 样例说明
 **样例 1:**

```
输入: ["(", "5", "-", "6", ")", "*", "7"]
输出: ["*", "-", "5", "6", "7"]
解释: (5 - 6) * 7 = -1 * 7 = -7
    * - 5 6 7 = * -1 7 = -7
```

**样例 2:**

```
输入: ["3", "+", "(", "1", "-", "2", ")"]
输出: ["+", "3", "-", "1", "2"] 
解释: 3 + (1 - 2) = 3 + -1 = 2
    + 3 - 1 2 = + 3 -1 = 2
```
 ### 参考代码
 借助 **栈** 我们可以实现中缀表达式到前缀表达式(即波兰表达式, PN)的转换.

从右到左遍历中缀表达式:

1. 如果碰到 **数字**, 直接追加到 PN 末尾.
2. 如果碰到 **右括号**, 入栈
3. 如果碰到 **左括号**, 弹栈, 并将弹出的元素依次追加到 PN 末尾, 直至右括号弹出(右括号不追加至PN)
4. 如果碰到 **运算符**, 弹栈直至栈顶元素优先级 **不大于** 当前运算符, 所有弹出的元素依次追加到 PN 末尾, 最后再将该运算符入栈

出于方便, 我们设定所有元素的优先级: `*/` 最高, `+-` 次之, 然后是数字, 最后是括号.

(把括号设为最低是因为, 碰到运算符弹栈时, 遇到括号也要停止, 所以可以直接设为最低)

遍历完后, 如果栈中还剩元素, 依次弹栈, 追加到 PN 末尾. 最后, 我们再将 PN 翻转, 就得到了正确的结果.
```python
class Solution:
    """
    @param expression: A string array
    @return: The Polish notation of this expression
    """
    def convertToPN(self, expression):
        stk = []
        PN = []
        for s in expression[::-1]:
            if s == ')':
                stk.append(s)
            elif s == '(':
                pos = stk[::-1].index(')')
                PN += stk[::-1][:pos]
                stk = stk[:-pos-1]
            elif s[0] in '1234567890':
                PN.append(s)
            else:
                priority = self.getPriority(s)
                while len(stk) and self.getPriority(stk[-1]) > priority:
                    PN.append(stk[-1])
                    stk.pop()
                stk.append(s)
        PN += stk[::-1]
        return PN[::-1]
    
    def getPriority(self, s):
        if s in '*/':
            return 3 
        if s in '+-':
            return 2 
        if s in '()':
            return 1 
        return 0

# 解法 2
class Solution:
    # @param m: An integer m denotes the size of a backpack
    # @param A: Given n items with size A[i]
    def opOrder(self, op1, op2):
        order_dic = {'*': 4, '/': 4, '+': 3, '-': 3}
        if op1 == '(' or op2 == '(':
            return False
        elif op2 == ')':
            return True
        else:
            if order_dic[op1] <= order_dic[op2]:
                return False
            else:
                return True

    def convertToPN(self, expression):
        prefix = []
        stack = []
        string_tmp = []
        for s in expression[::-1]:
            if s == '(':
                string_tmp.append(')')
            elif s == ')':
                string_tmp.append('(')
            else:
                string_tmp.append(s)

        for s in string_tmp:
            if s.isdigit():
                prefix = [s] + prefix
            else:
                while len(stack) and self.opOrder(stack[-1], s):
                    op = stack.pop()
                    prefix = [op] + prefix
                if len(stack) == 0 or s != ')':
                    stack.append(s)
                else:
                    stack.pop()
        if len(stack):
            prefix = stack + prefix

        return prefix
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)