# 合并排序数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/merge-sorted-array/?utm_source=sc-github-wzz)
 ## 题目描述
 合并两个排序的整数数组A和B变成一个新的数组。
 ### 样例说明
 **样例 1:**
```
输入：[1, 2, 3]  3  [4,5]  2
输出：[1,2,3,4,5]
解释:
经过合并新的数组为[1,2,3,4,5]
```
**样例 2:**
```
输入：[1,2,5] 3 [3,4] 2
输出：[1,2,3,4,5]
解释：
经过合并新的数组为[1,2,3,4,5]
```
 ### 参考代码
 Given two sorted integer arrays A and B, merge B into A as one sorted array.
考点：
* 双指针

Note:
You may assume that A has enough space (size that is greater or equal to m + n) to hold additional elements from B. The number of elements initialized in A and B are m and n respectively.
分析:涉及两个有序数组合并,设置i和j双指针,分别从两个数组的尾部想头部移动,并判断A[i]和B[j]的大小关系,从而保证最终数组有序,同时每次index从尾部向头部移动。
```java
class Solution {
    /**
     * @param A: sorted integer array A which has m elements, 
     *           but size of A is m+n
     * @param B: sorted integer array B which has n elements
     * @return: void
     */
    public void mergeSortedArray(int[] A, int m, int[] B, int n) {
        int i = m-1, j = n-1, index = m + n - 1;
        while (i >= 0 && j >= 0) {
            if (A[i] > B[j]) {
                A[index--] = A[i--];
            } else {
                A[index--] = B[j--];
            }
        }
        while (i >= 0) {
            A[index--] = A[i--];
        }
        while (j >= 0) {
            A[index--] = B[j--];
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)