# 两个排序数组的中位数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/median-of-two-sorted-arrays/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="line-height: 1.42857143;">两个排序的数组</span><span style="line-height: 1.42857143;">A和B</span><span style="line-height: 1.42857143;">分别含有m和n个数，找到两个排序数组的中位数，要求时间复杂度应为O(log (m+n))。</span></p>
 ### 样例说明
 **样例1**

```plain
输入:
A = [1,2,3,4,5,6]
B = [2,3,4,5]
输出: 3.5
```

**样例2**

```plain
输入:
A = [1,2,3]
B = [4,5]
输出: 3
```


 ### 参考代码
 分治法。时间复杂度 $log(n + m)$
```java
public class Solution {
    public double findMedianSortedArrays(int A[], int B[]) {
        int n = A.length + B.length;
        
        if (n % 2 == 0) {
            return (
                findKth(A, 0, B, 0, n / 2) + 
                findKth(A, 0, B, 0, n / 2 + 1)
            ) / 2.0;
        }
        
        return findKth(A, 0, B, 0, n / 2 + 1);
    }

    // find kth number of two sorted array
    public static int findKth(int[] A, int startOfA,
                              int[] B, int startOfB,
                              int k){       
        if (startOfA >= A.length) {
            return B[startOfB + k - 1];
        }
        if (startOfB >= B.length) {
            return A[startOfA + k - 1];
        }

        if (k == 1) {
            return Math.min(A[startOfA], B[startOfB]);
        }
        
        int halfKthOfA = startOfA + k / 2 - 1 < A.length
            ? A[startOfA + k / 2 - 1]
            : Integer.MAX_VALUE;
        int halfKthOfB = startOfB + k / 2 - 1 < B.length
            ? B[startOfB + k / 2 - 1]
            : Integer.MAX_VALUE; 
        
        if (halfKthOfA < halfKthOfB) {
            return findKth(A, startOfA + k / 2, B, startOfB, k - k / 2);
        } else {
            return findKth(A, startOfA, B, startOfB + k / 2, k - k / 2);
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)