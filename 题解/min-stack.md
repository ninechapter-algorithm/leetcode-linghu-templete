# 带最小值操作的栈
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/min-stack/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个栈, 支持以下操作:

- `push(val)` 将 val 压入栈
- `pop()` 将栈顶元素弹出, 并返回这个弹出的元素
- `min()` 返回栈中元素的最小值 

要求 O(1) 开销.
 ### 样例说明
 **样例 2:**

```
输入: 
  push(1)
  min()
  push(2)
  min()
  push(3)
  min()
输出: 
  1
  1
  1
```
 ### 参考代码
 使用两个仅支持 `pop` 和 `push` 的栈就可以完成, `stack` 储存压入的数据, `minStack` 储存最小值.

- `push` 直接把元素压入 stack, 对于 minStack, 如果它为空则直接压入, 反之压入当前元素与 minStack 栈顶的最小值
- `pop` 两个栈都弹出一个元素, 返回 stack 弹出的元素
- `min` 返回 minStack 的栈顶

> 还可以令 minStack 为单调栈, 即`push`时只有元素更小的时候才放入这个栈, 而`pop`时只有栈顶与stack栈顶相同时才弹出
> 
> 这样可以节约一定的空间, 但是实质上空间复杂度仍然是 O(n), 且多了一些判断, 并不一定更优
```java
// version 1:
public class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;
    
    public MinStack() {
        stack = new Stack<Integer>();
        minStack = new Stack<Integer>();
    }

    public void push(int number) {
        stack.push(number);
        if (minStack.isEmpty()) {
            minStack.push(number);
        } else {
            minStack.push(Math.min(number, minStack.peek()));
        }
    }

    public int pop() {
        minStack.pop();
        return stack.pop();
    }

    public int min() {
        return minStack.peek();
    }
}

// version 2, save more space. but space complexity doesn't change.
public class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    public MinStack() {
        stack = new Stack<Integer>();
        minStack = new Stack<Integer>();
    }

    public void push(int number) {
        stack.push(number);
        if (minStack.empty() == true)
            minStack.push(number);
        else if (minStack.peek() >= number) // 这里考虑的相等的情况也会继续push
            minStack.push(number);
    }

    public int pop() {
        if (stack.peek().equals(minStack.peek()))
            minStack.pop();
        return stack.pop();
    }

    public int min() {
        return minStack.peek();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)