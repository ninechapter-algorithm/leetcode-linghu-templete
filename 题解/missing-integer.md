# 丢失的数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/missing-integer/?utm_source=sc-github-wzz)
 ## 题目描述
 在数组 A 中，包含 0 到 n 的整数，其中缺失了一个数。在这一问题中，我们难以仅用一个操作审查数组 A 中的所有整数。 A 中的元素用二进制表示，而唯一可实现的操作是使用固定时间的操作 - `"fetch the jth bit of A[i]"` 。请编写代码，以查找数组中缺失的整数。你可以在 `O(n)` 的时间复杂度实现吗？
 ### 样例说明
 
**样例 1：**
```
输入：[4,3,2,0,5]
输出：1
```
**样例 2：**
```
输入：[0,1,2,3,4,7,6]
输出：5
```
 ### 参考代码
 ```java
/**
 * Definition of BitInteger:
 * public class BitInteger {
 *     public static int INTEGER_SIZE = 31;
 *     public int fetch(int j) {
 *         .... // return 0 or 1, fetch the jth bit of this number
 *     }
 * }
 */
public class Solution {
    /**
     * @param array a BitInteger list
     * @return an integer
     */
    public int findMissing(ArrayList<BitInteger> array) {
        // Write your code here
        /* Start from the least significant bit, and work our way up */
        return findMissing(array, 0);
    }

    public int findMissing(ArrayList<BitInteger> input, int column) {
        if (column >= BitInteger.INTEGER_SIZE) { // We're done!
            return 0;
        }
        ArrayList<BitInteger> oneBits = new ArrayList<BitInteger>();
        ArrayList<BitInteger> zeroBits = new ArrayList<BitInteger>();
        for (BitInteger t : input) {
            if (t.fetch(column) == 0) {
                zeroBits.add(t);
            } else {
                oneBits.add(t);
            }
        }
        
        if (zeroBits.size() <= oneBits.size()) {
            int v = findMissing(zeroBits, column + 1);
            return (v << 1) | 0;
        } else {
            int v = findMissing(oneBits, column + 1);
            return (v << 1) | 1;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)