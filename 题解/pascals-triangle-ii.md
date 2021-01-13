# 杨辉三角形II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/pascals-triangle-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定非负索引k，其中k≤33，返回杨辉三角形的第k个索引行。
 ### 样例说明
 **样例1**

```
输入: 3
输出: [1,3,3,1]
```

**样例2**

```
输入: 4
输出: [1,4,6,4,1]
```
 ### 参考代码
 Given an index k, return the kth row of the Pascal's triangle.

For example, given k = 3,
Return [1,3,3,1].

Note:
Could you optimize your algorithm to use only O(k) extra space?
```java
public class Solution {
    public ArrayList<Integer> getRow(int rowIndex) {
        ArrayList<Integer> rst = new ArrayList<Integer>();
        rowIndex += 1;
        if (rowIndex == 0) {
            return rst;
        }

        rst.add(1);
        for (int i = 1; i < rowIndex; i++) {
            ArrayList<Integer> tmp = new ArrayList<Integer>(i+1);
            for (int j = 0; j < i + 1; j++) {
                tmp.add(-1);
            }
            tmp.set(0, rst.get(0));
            tmp.set(i, rst.get(i - 1));
            for (int j = 1; j < i; j++) {
                tmp.set(j, rst.get(j - 1) + rst.get(j));
            }
            rst = tmp;
        }
        return rst;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)