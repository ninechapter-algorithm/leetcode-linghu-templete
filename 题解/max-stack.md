# 最大栈
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/max-stack/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一个支持push，pop，top，peekMax和popMax操作的最大栈。

1. push(x) -- 将元素x添加到栈中。
2. pop() -- 删除栈中最顶端的元素并将其返回。
3. top() -- 返回栈中最顶端的元素。
4. peekMax() -- 返回栈中最大的元素。
5. popMax() -- 返回栈中最大的元素，并将其删除。如果有多于一个最大的元素，只删除最靠近顶端的一个元素。
 ### 样例说明
 ```
输入:
push(5)
push(1)
push(5)
top()
popMax()
top()
peekMax()
pop()
top()
输出:
5
5
1
5
1
5
```
 ### 参考代码
 ```python
class MaxStack:

    def __init__(self):
        self.stack = []
        self.max_stack = []
        
    def push(self, x):
        self.stack.append(x)
        if self.max_stack:
            number = max(self.max_stack[-1], x)
            self.max_stack.append(number)
        else:
            self.max_stack.append(x)

    def pop(self):
        self.max_stack.pop()
        return self.stack.pop()

    def top(self):
        return self.stack[-1]

    def peekMax(self):
        return self.max_stack[-1]

    def popMax(self):
        max_number = self.peekMax()
        buffer_stack = []
        while self.top() != max_number:
            buffer_stack.append(self.pop())
        self.pop()
        while buffer_stack:
            self.push(buffer_stack[-1])
            buffer_stack.pop()
        return max_number
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)