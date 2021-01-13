# 摊平嵌套的列表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/flatten-nested-list-iterator/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个嵌套的列表，实现一个迭代器将其摊平。
一个列表的每个元素可能是整数或者一个列表。
 ### 样例说明
 **样例1**

```
输入: list = [[1,1],2,[1,1]]
输出: [1,1,2,1,1]
```

**样例2**

```
输入: list = [1,[4,[6]]]
输出: [1,4,6]
```
 ### 参考代码
 直接枚举列表中的每个数字，然后将这些数字依次放到另一个数组中返回
```java
import java.util.Iterator;

public class NestedIterator implements Iterator<Integer> {

    private Stack<NestedInteger> stack;
    
    private void pushListToStack(List<NestedInteger> nestedList) {
        Stack<NestedInteger> temp = new Stack<>();
        for (NestedInteger nested : nestedList) {
            temp.push(nested);
        }
        
        while (!temp.isEmpty()) {
            stack.push(temp.pop());
        }
    }
    
    public NestedIterator(List<NestedInteger> nestedList) {
        stack = new Stack<>();
        pushListToStack(nestedList);
    }

    // @return {int} the next element in the iteration
    @Override
    public Integer next() {
        if (!hasNext()) {
            return null;
        }
        return stack.pop().getInteger();
    }

    // @return {boolean} true if the iteration has more element or false
    @Override
    public boolean hasNext() {
        while (!stack.isEmpty() && !stack.peek().isInteger()) {
            pushListToStack(stack.pop().getList());
        }
        
        return !stack.isEmpty();
    }
    
    @Override
    public void remove() {}
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)