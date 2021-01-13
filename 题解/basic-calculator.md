# 基础计算器
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/basic-calculator/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个基础的计算器来计算一个简单表达式。

这个表达式字符串可能包含左括号 `'('` 与右括号 `')'`，加号 `'+'` 或者 减号 `'-'`，**非负**整数以及空格 `' '`。

给出的表达式总是合理的。
 ### 样例说明
 **样例 1**
```
输入："1 + 1"
输出：2
```
**样例 2**
```
输入："(1+(4+5+2)-3)+(6+8)" 
输出：23
```
 ### 参考代码
 ```
[[python]]
class Solution:
    """
    @param s: the expression string
    @return: the answer
    """
    def calculate(self, s):
        expression = []
        val = None
        for char in s:
            if char == ' ':
                continue
            if char in ['+', '-', '*', '/', '(', ')']:
                if val is not None:
                    expression.append(str(val))
                expression.append(char)
                val = None
            else:
                if val is None:
                    val = 0
                val = val * 10 + ord(char) - ord('0')
        if val is not None:
            expression.append(str(val))
        
        return self.evaluate_expression(expression)

    def evaluate_expression(self, expression):
        if not expression:
            return 0
        if len(expression) == 1:
            return int(expression[0])
            
        can_divide, total = self.divide_expression(expression, ['+', '-'])
        if can_divide:
            return total
    
        can_divide, total = self.divide_expression(expression, ['*', '/'])
        if can_divide:
            return total
            
        # must be parens around the expression
        return self.evaluate_expression(expression[1:-1])
            
    def divide_expression(self, expression, operators):
        last_index, parens = 0, 0
        last_operator = operators[0]
        total = 1 if last_operator == '*' else 0
        can_divide = False
        
        for index, elem in enumerate(expression):
            if elem in operators and parens == 0:
                can_divide = True
                val = self.evaluate_expression(expression[last_index: index])
                total = self.calc(total, last_operator, val)
                last_operator = elem
                last_index = index + 1
            elif elem == '(':
                parens += 1
            elif elem == ')':
                parens -= 1
        
        if can_divide:
            val = self.evaluate_expression(expression[last_index:])
            total = self.calc(total, last_operator, val)
            
        return can_divide, total
     
    def calc(self, a, operator, b):
        if operator == '+':
            return a + b
        elif operator == '-':
            return a - b
        elif operator == '*':
            return a * b
        else:
            return a // b
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)