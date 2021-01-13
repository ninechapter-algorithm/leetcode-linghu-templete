# 列表扁平化
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/flatten-list/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个列表，该列表中的每个元素要么是个列表，要么是整数。将其变成一个只包含整数的简单列表。
 ### 样例说明
 ```
样例  1:
	输入: [[1,1],2,[1,1]]
	输出:[1,1,2,1,1] 
	
	样例解释:
	将其变成一个只包含整数的简单列表。


样例 2:
	输入: [1,2,[1,2]]
	输出:[1,2,1,2]
	
	样例解释: 
	将其变成一个只包含整数的简单列表。
	
样例 3:
	输入:[4,[3,[2,[1]]]]
	输出:[4,3,2,1]
	
	样例解释: 
	将其变成一个只包含整数的简单列表。
	
```

 ### 参考代码
 递归处理，每碰到列表就递归处理，每碰到一个数字就添加进答案数组中。

复杂度O(n)
```java
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

    // @param nestedList a list of NestedInteger
    // @return a list of integer
    public List<Integer> flatten(List<NestedInteger> nestedList) {
        // Write your code here
        List<Integer> result = new ArrayList<Integer>();
        for (NestedInteger ele : nestedList)
            if (ele.isInteger())
                result.add(ele.getInteger());
            else
                result.addAll(flatten(ele.getList()));
        return result;
    }
}

//non-recursive version
public class Solution {

    // @param nestedList a list of NestedInteger
    // @return a list of integer
    public List<Integer> flatten(List<NestedInteger> nestedList) {
        boolean isFlat = true;
        List<NestedInteger> ls = nestedList;
        while (isFlat) {
            isFlat = false;
            List<NestedInteger> newLs = new ArrayList<>();
            for (NestedInteger ni : ls) {
                if (ni.isInteger()) {
                    newLs.add(ni);
                } else {
                    newLs.addAll(ni.getList());
                    isFlat = true;
                }
            }
            ls = newLs;
        }
        List<Integer> r = new ArrayList<>();
        for (NestedInteger ni : ls) {
            r.add(ni.getInteger());
        }
        return r;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)