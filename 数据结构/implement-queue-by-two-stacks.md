# 用栈实现队列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/implement-queue-by-two-stacks/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="line-height: 1.42857143;">正如标题所述，你需要使用两个栈来实现队列的一些操作。</span><br></p><p>队列应支持push(element)，pop() 和 top()，其中pop是弹出队列中的第一个(最前面的)元素。</p><p>pop和top方法都应该返回第一个元素的值。<br></p>
 ### 样例说明
 **例1:**

```
输入:
    push(1)
    pop()    
    push(2)
    push(3)
    top()    
    pop()     
输出:
    1
    2
    2
```

**例2:**

```
输入:
    push(1)
    push(2)
    push(2)
    push(3)
    push(4)
    push(5)
    push(6)
    push(7)
    push(1)
输出:
[]
```


 ### 参考代码
 push加入到栈中
top即从A栈出到B栈，执行完之后，B栈push出栈顶元素，作为返回值，然后继续入站栈，最后B栈出，返回A栈。
pop即从A栈出到B栈，执行完之后，B栈push出栈顶元素，然后B栈依次出，返回A栈。
```java
public class MyQueue {
    private Stack<Integer> stack1;
    private Stack<Integer> stack2;

    public MyQueue() {
       stack1 = new Stack<Integer>();
       stack2 = new Stack<Integer>();
    }
    
    private void stack2ToStack1(){
        while(! stack2.isEmpty()){
            stack1.push(stack2.pop());
        }
    }
    
    public void push(int element) {
        stack2.push(element);
    }

    public int pop() {
        if(stack1.empty() == true){
            this.stack2ToStack1();
        }
        return stack1.pop();
    }

    public int top() {
        if(stack1.empty() == true){
            this.stack2ToStack1();
        }
        return stack1.peek();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)