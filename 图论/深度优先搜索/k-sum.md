# K数之和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/k-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定 *n* 个不同的正整数，整数 *k*（*k* <= *n*）以及一个目标数字 *target*。　
在这 *n* 个数里面找出 *k* 个数，使得这 *k* 个数的和等于目标数字，求问有多少种方案？
 ### 样例说明
 **样例1**

```plain
输入:
List = [1,2,3,4]
k = 2
target = 5
输出: 2
说明: 1 + 4 = 2 + 3 = 5
```

**样例2**

```plain
输入:
List = [1,2,3,4,5]
k = 3
target = 6
输出: 1
说明: 只有这一种方案。 1 + 2 + 3 = 6
```


 ### 参考代码
 采用动态规划（dp）的思想，进行状态转移，记录数字和和出现次数之间的关系。
用$dp[i][j][k]$表示前$i$个数里选$j$个和为$k$的方案数。
```java
public class Solution {
    /**
     * @param A: an integer array.
     * @param k: a positive integer (k <= length(A))
     * @param target: a integer
     * @return an integer
     */
    public int  kSum(int A[], int k, int target) {
        int n = A.length;
        int[][][] f = new int[n + 1][k + 1][target + 1];
        for (int i = 0; i < n + 1; i++) {
            f[i][0][0] = 1;
        }
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= k && j <= i; j++) {
                for (int t = 1; t <= target; t++) {
                    f[i][j][t] = 0;
                    if (t >= A[i - 1]) {
                        f[i][j][t] = f[i - 1][j - 1][t - A[i - 1]];
                    }
                    f[i][j][t] += f[i - 1][j][t];
                } // for t
            } // for j
        } // for i
        return f[n][k][target];
    }
}

// 九章动态规划专题班
// 打印所有方案版本
public class Solution {
    /**
     * @param A: An integer array
     * @param k: A positive integer (k <= length(A))
     * @param target: An integer
     * @return: An integer
     */
     
    int[] res;
    int tot;
    int[] A;
    int K;
    int[][][] f;
    
    void printAnswer(int i, int j, int k) {
        if (j == 0) {
            for (int h = 0; h < K; ++h) {
                System.out.print(res[h]);
                if (h == K - 1) {
                    System.out.println("=" + tot);
                }
                else {
                    System.out.print("+");
                }
            }
            
            return;
        }
        
        if (f[i - 1][j][k] > 0) {
            printAnswer(i - 1, j, k);
        }
        
        if (j > 0 && k >= A[i - 1] && f[i - 1][j - 1][k - A[i - 1]] > 0) {
            res[j - 1] = A[i - 1];
            printAnswer(i - 1, j - 1, k - A[i - 1]);
        }
    }
    
    public int kSum(int[] AA, int KK, int T) {
        K = KK;
        A = AA;
        int n = A.length;
        res = new int[K];
        tot = T;
        f = new int[n + 1][K + 1][T + 1];
        int i, j, k;
        for (j = 0; j <= K; ++j) {
            for (k = 0; k <= T; ++k) {
                f[0][j][k] = 0;
            }
        }
        
        f[0][0][0] = 1;
        for (i = 1; i <= n; ++i) {
            for (j = 0; j <= K; ++j) {
                for (k = 0; k <= T; ++k) {
                    // not using A[i - 1]
                    f[i][j][k] = f[i - 1][j][k];
                    
                    // using A[i - 1]
                    if (j > 0 && k >= A[i - 1]) {
                        f[i][j][k] += f[i - 1][j - 1][k - A[i - 1]];
                    }
                }
            }
        }
        
        printAnswer(n, K, T);
        
        return f[n][K][T];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)