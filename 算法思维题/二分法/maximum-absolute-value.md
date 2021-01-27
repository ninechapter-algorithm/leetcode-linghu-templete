# 最大绝对值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-absolute-value/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组`A`，从中选出`n`个数，使得这个`n`个数中两两之差的绝对值的最小值尽可能大。你需要返回这个最大的绝对值。
 ### 样例说明
 **样例1**

```
输入: A = [1,2,8,4,9,3], n = 3
输出: 3
解释:
选择[1,4,8]或者[1,4,9]均可。
```

**样例2**

```
输入: A = [1,2,3,4,5,6],  n = 2
输出: 5
解释:
选[1,6]
```
 ### 参考代码
 二分答案，类似 Wood Cut
```java
public class Solution {
    /**
     * @param A: an array
     * @param n: an integer
     * @return: makes the smallest absolute value of the difference between any two elements to largest
     */
    public int maximumAbsolutValue(int[] A, int n) {
        if (A == null || A.length == 0) {
            return -1;
        }
        
        Arrays.sort(A);
        
        // find maximum gap that we can get more than n numbers
        int start = 0, end = 2147483647;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (getNumbers(A, mid) >= n) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (getNumbers(A, end) >= n) {
            return end;
        }
        
        return start;
    }

    // greedy algorithm to get the most numbers from array
    private int getNumbers(int[] A, int gap) {
        int count = 1, lastNumber = A[0];
        for (int i = 1; i < A.length; i++) {
            if (A[i] - lastNumber >= gap) {
                lastNumber = A[i];
                count++;
            }
        }
        return count;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)