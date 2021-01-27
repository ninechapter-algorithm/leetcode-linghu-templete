# 实现栈
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/implement-stack/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个栈，可以使用除了栈之外的数据结构
 ### 样例说明
 例1:
```
输入：
push(1)
pop()
push(2)
top()  // return 2
pop()
isEmpty() // return true
push(3)
isEmpty() // return false
```
例2:
```
输入：
isEmpty()

```
 ### 参考代码
 实现栈的基本操作
```java
class Stack {
    // Push a new item into the stack
    public void push(int x) {
        // Write your code here
        array.add(x);
    }

    // Pop the top of the stack
    public void pop() {
        // Write your code here
        int n = array.size();
        if (n > 0)
            array.remove(n-1);
        return;
    }

    // Return the top of the stack
    public int top() {
        // Write your code here
        int n = array.size();
        return array.get(n-1);
    }

    // Check the stack is empty or not.
    public boolean isEmpty() {
        // Write your code here
        return array.size() == 0;
    }

    private List<Integer> array = new ArrayList<Integer>();
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)