# 统计前面比自己小的数的个数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/count-of-smaller-number-before-itself/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组（下标由 0 到 n-1， n 表示数组的规模，取值范围由 0 到10000）。对于数组中的每个 `ai` 元素，请计算 `ai` 前的数中比它小的元素的数量。
 ### 样例说明
 **样例 1:**
```
输入:
[1,2,7,8,5]
输出:
[0,1,2,3,2]
```

**样例 2:**
```
输入:
[7,8,2,1,3]
输出:
[0,1,0,0,2]
```
 ### 参考代码
 使用 Fenwick Tree （Binary Indexed Tree） 的解法
```java
class BITree {
    public int[] bit;

    public BITree(int range) {
        bit = new int[range + 1];
    }
    
    public void increase(int index, int delta) {
        for (int i = index + 1; i < bit.length; i = i + lowbit(i)) {
            bit[i] += delta;
        }
    }
    
    public int getPrefixSum(int index) {
        int sum = 0;
        for (int i = index + 1; i >= 1; i = i - lowbit(i)) {
            sum += bit[i];
        }
        return sum;
    }
    
    private int lowbit(int x) {
        return x & (-x);
    }
}

public class Solution {
    /**
     * @param A: an integer array
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    public List<Integer> countOfSmallerNumberII(int[] A) {
        BITree bitree = new BITree(10000);
        List<Integer> results = new ArrayList<>();
        for (int i = 0; i < A.length; i++) {
            results.add(bitree.getPrefixSum(A[i] - 1));
            bitree.increase(A[i], 1); 
        }
        
        return results;
    }
    
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)