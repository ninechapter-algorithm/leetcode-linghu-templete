# 嵌套列表的加权和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/nested-list-weight-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个嵌套的整数列表, 返回列表中所有整数由它们的深度加权后的总和. 每一个元素可能是一个整数或一个列表(其元素也可能是整数或列表)
 ### 样例说明
 例1:
```
输入: the list [[1,1],2,[1,1]], 
输出: 10. 
解释:
four 1's at depth 2, one 2 at depth 1, 4 * 1 * 2 + 1 * 2 * 1 = 10
```
例2:
```
输入: the list [1,[4,[6]]], 
输出: 27. 
解释:
one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4 * 2 + 6 * 3 = 27
```

 ### 参考代码
 dfs按照深度带权求和
```java
// 递归
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer,
 *     // rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds,
 *     // if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds,
 *     // if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class Solution {
    
    public int depthSum(List<NestedInteger> nestedList) {
        return helper(nestedList, 1);
    }
 
    public int helper(List<NestedInteger> nestedList, int depth){
        if (nestedList == null || nestedList.size() == 0)
            return 0;

        int sum = 0;
        for(NestedInteger ele : nestedList) {
            if (ele.isInteger()) {
                sum += ele.getInteger() * depth;
            } else {
                sum += helper(ele.getList(), depth + 1);
            }
        }
 
        return sum;
    }
}

// 非递归
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer,
 *     // rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds,
 *     // if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds,
 *     // if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class Solution {
    public int depthSum(List<NestedInteger> nestedList) {
        // Write your code here
        if (nestedList == null || nestedList.size() == 0) {
            return 0;
        }
        int sum = 0;
        Queue<NestedInteger> queue = new LinkedList<NestedInteger>();
        for (NestedInteger nestedInt : nestedList) {
            queue.offer(nestedInt);
        }

        int depth = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            depth++;
            for (int i = 0; i < size; i++) {
                NestedInteger nestedInt = queue.poll();
                if (nestedInt.isInteger()) {
                    sum += nestedInt.getInteger() * depth;
                } else {
                    for (NestedInteger innerInt : nestedInt.getList()) {
                        queue.offer(innerInt);
                    }
                }
            }
        }
        return sum;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)