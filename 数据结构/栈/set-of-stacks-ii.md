# 栈集II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/set-of-stacks-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 假如你有一堆的盘子。如果你堆得太高的话，就可能会垮掉。所以，在真实的生活中，如果盘子叠到一定高度，你会重新开始堆新的一堆盘子。

实现这样的一个数据结构，我们称之为栈集，来模拟这个过程。这个栈集包含若干个栈（可以理解为若干堆的盘子），如果一个栈满了，就需要新建一个栈来装新加入的项。你需要实现栈集的两个方法，`push(item)` 和 `pop()`，让这个栈集对外表现得就像是一个栈在进行操作一样。

另外，你还需要多实现一个`popAt(index)`的方法，该方法可以pop栈集中指定的栈的栈顶元素。并且，该方法执行后，除了，最后一个栈可以不满以外，其他的栈仍然需要保持是满的。
 ### 样例说明
 **样例1**

```plain
输入:
SetOfStacks(2)
push(1)
push(2)
push(4)
push(8)
push(16)
popAt(0) 
popAt(0) 
pop()    

输出:
[2,4,16]

解释:
起初，堆栈0是[1,2]。 当popAt(0)时, 我们得到2然后栈变成[1,4]. 
在整个栈里，我们应该pop16。
```



**样例2**

```plain
输入:
SetOfStacks2(5)
push(1)
push(2)
push(3)
push(4)
push(5)
push(32)
pop()
push(64)
popAt(1)

输出:
[32,64]

说明:
开始栈0是[32]. 当pop的时候我们取出32然后栈变空了。
然后我们放入64，它被放在栈1，我们 popAt(1) 取出它。
```


 ### 参考代码
 本题考查栈的模拟应用，按照题目要求进行分组，然后取出或者加入对应元素即可。
```java
public class SetOfStacks2 {
    ArrayList<Stack> stacks = new ArrayList<Stack>();
    public int capacity;
    // @param capacity an inetger, capacity of sub stack
    public SetOfStacks2(int capacity) {
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
	
    // popAt which performs a pop operation on a specific sub-stack
    // @return top element of the specific sub-stack
    public int popAt(int index) {
        // Write your code here
        return leftShift(index, true);
    }
	
    public int leftShift(int index, boolean removeTop) {
        Stack stack = stacks.get(index);
        int removed_item;
        if (removeTop) removed_item = stack.pop();
        else removed_item = stack.removeBottom();
        if (stack.isEmpty()) {	
            stacks.remove(index);
        } else if (stacks.size() > index + 1) {
            int v = leftShift(index + 1, false);
		    stack.push(v);	
        }
        return removed_item;
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