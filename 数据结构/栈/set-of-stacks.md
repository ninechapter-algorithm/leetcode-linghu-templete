# 栈集
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/set-of-stacks/?utm_source=sc-github-wzz)
 ## 题目描述
 假如你有一堆的盘子。如果你堆得太高的话，就可能会垮掉。所以，在真实的生活中，如果盘子叠到一定高度，你会重新开始堆新的一堆盘子。

实现这样的一个数据结构，我们称之为`栈集`，来模拟这个过程。这个栈集包含若干个栈（可以理解为若干堆的盘子），如果一个栈满了，就需要新建一个栈来装新加入的项。你需要实现栈集的两个方法，`push(item)` 和 `pop()`，让这个栈集对外表现得就像是一个栈在进行操作一样。
 ### 样例说明
 例1:
```
输入：
SetOfStacks(2);  // create a SetOfStacks object with capacity = 2
push(1)
push(2)
push(4)
push(8)
push(16)
pop() // return 16
pop() // return 8
pop() // return 4
```

例2:
```
输入：
SetOfStacks(5)  
push(1)
push(2)
push(3)
push(4)
push(5)
push(32)
pop()  // return 32
push(64)
pop()  // return 64

```
 ### 参考代码
 若当前栈满，开辟一个新的栈加入到vector中或链表中，若当前栈空，取出这个栈即可
```java
public class SetOfStacks {
    ArrayList<Stack> stacks = new ArrayList<Stack>();
    public int capacity;
    // @param capacity an inetger, capacity of sub stack
    public SetOfStacks(int capacity) {
        // do initialization if necessary
        this.capacity = capacity;
    }
    public Stack getLastStack() {	
        if (stacks.size() == 0) return null;
            return stacks.get(stacks.size() - 1);
    }
	
    // @param v an integer
    public void push(int v) {
        // Write your code here
        Stack last = getLastStack();
        if (last != null && !last.isAtCapacity()) { // add to last stack
            last.push(v);
        } else { // must create new stack
		    Stack stack = new Stack(capacity);
            stack.push(v);
            stacks.add(stack);
        }
    }
	
    // @return an integer
    public int pop() {
        // Write your code here
        Stack last = getLastStack();
        int v = last.pop();
        if (last.size == 0) stacks.remove(stacks.size() - 1);
            return v;
    }
}

class Stack {
    private int capacity;
    public Node top, bottom;
    public int size = 0;
    public Stack(int capacity) { this.capacity = capacity; }
    public boolean isAtCapacity() { return capacity == size; }
    public void join(Node above, Node below) {	
        if (below != null) below.above = above;
        if (above != null) above.below = below;	
    }
	
    public boolean push(int v) {	
        if (size >= capacity) return false;
		size++;		
        Node n = new Node(v);
        if (size == 1) bottom = n;
        join(n, top);
        top = n;
        return true;
    }
	
    public int pop() {	
        Node t = top;	
        top = top.below;
        size--;
        return t.value;
    }

    public boolean isEmpty() { return size == 0; }
    public int removeBottom() {	
        Node b = bottom;	
        bottom = bottom.above;	
        if (bottom != null) bottom.below = null;	
        size--;
        return b.value;	
    }
}

class Node {
    public Node below, above;
    public int value;
    Node(int v) {
        this.value = v;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)