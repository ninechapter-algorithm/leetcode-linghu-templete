# 维护队列 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/implement-queue-by-linked-list-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个双端队列
1. `push_front(item)`. 将新项添加到队列的前面。
2. `push_back(item)`. 将新项添加到队列的后面。
2. `pop_front()`. 将第一个项移出队列，返回它。
3. `pop_back()`. 将最后一项移出队列，返回它。
 ### 样例说明
 例1：
```
输入：
push_front(1)
push_back(2)
pop_back() // return 2
pop_back() // return 1
push_back(3)
push_back(4)
pop_front() // return 3
pop_front() // return 4
```

例2：
```
输入：
push_front(1)
pop_front()// return 1

```
 ### 参考代码
 实现双端队列的两头进出操作
```java
class Node {
    public int val;
    public Node next, prev;
    public Node(int _val) {
        val = _val;
        prev = next = null;
    }
}

public class Dequeue {
    public Node first, last;
    
    public Dequeue() {
        first = last = null;
        // do initialize if necessary
    }

    public void push_front(int item) {
        // Write your code here
        if (first == null) {
            last = new Node(item);
            first = last;		
        } else {
            Node tmp = new Node(item);
            first.prev = tmp;
            tmp.next = first;
            first = first.prev;
        }
    }

    public void push_back(int item) {
        // Write your code here
        if (last == null) {
            last = new Node(item);
            first = last;		
        } else {
            Node tmp = new Node(item);
            last.next = tmp;
            tmp.prev = last;
            last = last.next;
        }
    }

    public int pop_front() {
        // Write your code here
        if (first != null) {
            int item = first.val;
            first = first.next;
            if (first != null)
                first.prev = null;
            else
                last = null;
            return item;
        }
        return -11;
    }

    public int pop_back() {
        // Write your code here
        if (last != null) {
            int item = last.val;
            last = last.prev;
            if (last != null)
                last.next = null;
            else
                first = null;
            return item;
        }
        return -11;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)