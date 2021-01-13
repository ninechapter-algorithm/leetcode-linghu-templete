# 按接口实现队列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/implement-queue-by-interface/?utm_source=sc-github-wzz)
 ## 题目描述
 按接口实现队列
 ### 样例说明
 查看代码了解更多信息
 ### 参考代码
 按要求实现接口即可
```java
class Node {
    public int val;
    public Node next, prev;
    public Node(int _val) {
        val = _val;
        prev = next = null;
    }
}

interface InterfaceQueue {
    void push(int element);

    // define an interface for pop method
    /* write your code here */
    int pop();

    // define an interface for top method
    /* write your code here */
    int top();
}

public class MyQueue implements InterfaceQueue {
    /* you can declare your private attributes here */
    public Node first, last;

    public MyQueue() {
       // do initialization if necessary
    }

    // implement the push method
    /* write your code here */
    @Override
    public void push(int val) {
        if (last == null) {
            last = new Node(val);
            first = last;		
        } else {
            Node node = new Node(val);
            last.next = node;
            node.prev = last;
            last = last.next;
        }
    }

    @Override
    public int pop() {
        /* write your code here */
        if (first != null) {
            int val = first.val;
            first = first.next;
            if (first != null)
                first.prev = null;
            else
                last = null;
            return val;
        }
        return -1;
    }

    @Override
    public int top() {
        /* write your code here */
        if (first != null) {
            return first.val;
        }
        return -1;
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue queue = new MyQueue();
 * queue.push(123);
 * queue.top(); will return 123;
 * queue.pop(); will return 123 and pop the first element in the queue
 */
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)