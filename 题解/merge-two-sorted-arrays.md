# 合并排序数组 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/merge-two-sorted-arrays/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>合并两个有序升序的整数数组A和B变成一个新的数组。新数组也要有序。</p>
 ### 样例说明
 **样例  1:**

```
输入: A=[1], B=[1]
输出:[1,1]	
样例解释: 返回合并后的数组。
```

**样例 2:**

```
输入: A=[1,2,3,4], B=[2,4,5,6]
输出: [1,2,2,3,4,4,5,6]	
样例解释: 返回合并后的数组。
```
 ### 参考代码
 使用两个指针分别对数组从小到大遍历，每次取二者中较小的放在新数组中。
直到某个指针先到结尾，另一个数组中剩余的数字直接放在新数组后面。

时间复杂度O(n)
```java
class Solution {
    /**
     * @param A and B: sorted integer array A and B.
     * @return: A new sorted integer array
     */
    public int[] mergeSortedArray(int[] A, int[] B) {
        if (A == null || B == null) {
            return null;
        }
        
        int[] result = new int[A.length + B.length];
        int i = 0, j = 0, index = 0;
        
        while (i < A.length && j < B.length) {
            if (A[i] < B[j]) {
                result[index++] = A[i++];
            } else {
                result[index++] = B[j++];
            }
        }
        
        while (i < A.length) {
            result[index++] = A[i++];
        }
        while (j < B.length) {
            result[index++] = B[j++];
        }
        
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)