# 队列维护
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/implement-queue-by-linked-list/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个队列的操作

1. `enqueue(item)`.将新元素放入队列中。
2. `dequeue()`. 将第一个元素移出队列，返回它。
 ### 样例说明
 例1:
```
输入：
enqueue(1)
enqueue(2)
enqueue(3)
dequeue() // return 1
enqueue(4)
dequeue() // return 2
```
例2:
```
输入：
enqueue(10)
dequeue()// return 10

```
 ### 参考代码
 实现队列基本入队出队操作
```java
class Node {
    public int val;
    public Node next;
    public Node(int _val) {
        val = _val;
        next = null;
    }
}

public class MyQueue {
    public Node first, last;
    
    public Queue() {
        first = last = null;
        // do initialize if necessary
    }

    public void enqueue(int item) {
        // Write your code here
        if (first == null) {
            last = new Node(item);
            first = last;		
        } else {
            last.next = new Node(item);
            last = last.next;
        }
    }

    public int dequeue() {
        // Write your code here
        if (first != null) {
            int item = first.val;
            first = first.next;
            return item;
        }
        return -1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)