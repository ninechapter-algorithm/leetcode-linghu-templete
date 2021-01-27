# 双队列实现栈
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/implement-stack-by-two-queues/?utm_source=sc-github-wzz)
 ## 题目描述
 利用两个队列来实现一个栈的功能
 ### 样例说明
 例1:
```
输入：
push(1)
pop()
push(2)
isEmpty() // return false
top() // return 2
pop()
isEmpty() // return true
```

例2:
```
输入：
isEmpty()

```
 ### 参考代码
 通过另一队列的进出，可以将此队列改造为栈，实现栈的基本操作
```java
class Stack {
    private Queue<Integer> queue1;
    private Queue<Integer> queue2;
    
    public Stack() {
        queue1 = new LinkedList<Integer>();
        queue2 = new LinkedList<Integer>();
    }
    
    private void moveItems() {
        while (queue1.size() != 1) {
            queue2.offer(queue1.poll());
        }
    }
    
    private void swapQueues() {
        Queue<Integer> temp = queue1;
        queue1 = queue2;
        queue2 = temp;
    }
    
    /**
     * push a new item into the stack
     */
    public void push(int value) {
        queue1.offer(value);
    }
    
    /**
     * return the top of the stack
     */
    public int top() {
        moveItems();
        int item = queue1.poll();
        swapQueues();
        queue1.offer(item);
        return item;
    }
    
    /**
     * pop the top of the stack and return it
     */
    public void pop() {
        moveItems();
        queue1.poll();
        swapQueues();
    }
    
    /**
     * check the stack is empty or not.
     */
    public boolean isEmpty() {
        return queue1.isEmpty();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)