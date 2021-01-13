# 删除排序数组中的重复数字
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/remove-duplicates-from-sorted-array/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个排序数组，在原数组中“删除”重复出现的数字，使得每个元素只出现一次，并且返回“新”数组的长度。

不要使用额外的数组空间，必须在不使用额外空间的条件下原地完成。
 ### 样例说明
 **样例 1:**

```
输入:  []
输出: 0
```

**样例 2:**

```
输入:  [1,1,2]
输出: 2	
解释:  数字只出现一次的数组为: [1,2]
```
 ### 参考代码
 Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,
Given input array A = [1,1,2],

Your function should return length = 2, and A is now [1,2].

由于有序，所以相同的数字排在一起。
用一个游标变量指向已经去重的部分的下一个空位，只要$a[i] != a[i-1]$,就将a[i]填入之前的空位。
```java
public class Solution {
    public int removeDuplicates(int[] A) {
        if (A == null || A.length == 0) {
            return 0;
        }
        
        int size = 0;
        for (int i = 0; i < A.length; i++) {
            if (A[i] != A[size]) {
                A[++size] = A[i];
            }
        }
        return size + 1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)