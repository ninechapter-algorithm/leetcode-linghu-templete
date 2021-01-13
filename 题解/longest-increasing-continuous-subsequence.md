# 最长上升连续子序列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-increasing-continuous-subsequence/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组（下标从 0 到 n-1， n 表示整个数组的规模），请找出该数组中的最长上升连续子序列。（最长上升连续子序列可以定义为从右到左或从左到右的序列。）
 ### 样例说明
 
 ### 参考代码
 ```java
public class Solution {
    public int longestIncreasingContinuousSubsequence(int[] A) {
        if (A == null || A.length == 0) {
            return 0;
        }
        
        int n = A.length;
        int answer = 1;
        
        // from left to right
        int length = 1; // just A[0] itself
        for (int i = 1; i < n; i++) {
            if (A[i] > A[i - 1]) {
                length++;
            } else {
                length = 1;
            }
            answer = Math.max(answer, length);
        }
        
        // from right to left
        length = 1;
        for (int i = n - 2; i >= 0; i--) {
            if (A[i] > A[i + 1]) {
                length++;
            } else {
                length = 1;
            }
            answer = Math.max(answer, length);
        }
        
        return answer;
    }
}

//  方法二
public class Solution {
    /**
     * @param A an array of Integer
     * @return  an integer
     */
    
    int LIS(int[] A) {
        int n = A.length;
        int[] f = new int[n];
        int i, res = 0;
        for (i = 0; i < n; ++i) {
            f[i] = 1;
            if (i > 0 && A[i-1] < A[i]) {
                f[i] = f[i-1] + 1;
            }
            if (f[i] > res) {
                res = f[i];
            }
        }
        
        return res;
    }
     
    public int longestIncreasingContinuousSubsequence(int[] A) {
        int n = A.length;
        int r1 = LIS(A);
        int i = 0, j = n-1, t;
        while (i < j) {
            t = A[i];
            A[i] = A[j];
            A[j] = t;
            ++i;
            --j;
        }
        
        int r2 = LIS(A);
        
        if (r1 > r2) {
            return r1;
        }
        else {
            return r2;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)