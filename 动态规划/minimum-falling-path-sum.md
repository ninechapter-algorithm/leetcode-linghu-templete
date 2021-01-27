# 下降路径最小和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-falling-path-sum/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个**方形**整数数组 A，我们想要得到通过 A 的下降路径的**最小**和。

下降路径可以从第一行中的任何元素开始，并从每一行中选择一个元素。在下一行选择的元素和当前行所选元素最多相隔一列。
 ### 样例说明
 **样例：**

```
输入：[[1,2,3],[4,5,6],[7,8,9]]
输出：12
解释：
可能的下降路径有：
[1,4,7], [1,4,8], [1,5,7], [1,5,8], [1,5,9]

[2,4,7], [2,4,8], [2,5,7], [2,5,8], [2,5,9], [2,6,8], [2,6,9]

[3,5,7], [3,5,8], [3,5,9], [3,6,8], [3,6,9]

和最小的下降路径是 [1,4,7]，所以答案是 12。
```
 ### 参考代码
 ```
[[python]]
class Solution:
    """
    @param A: the given array
    @return: the minimum sum of a falling path
    """
    def minFallingPathSum(self, A):
        n, m = len(A), len(A[0])
        # state: dp[i][j] 表示从第一行走到 i,j 这个位置的最小路径和
        dp = [[0] * m, [0] * m]
        
        # initialization: dp[0][i] = A[0][i]
        for i in range(m):
            dp[0][i] = A[0][i]
        
        # function: dp[i][j] = min(dp[i - 1][j - 1], dp[i - 1][j], dp[i - 1][j + 1]) + A[i][j]
        for i in range(1, n):
            for j in range(0, m):
                dp[i % 2][j] = dp[(i - 1) % 2][j] + A[i][j]
                if j - 1 >= 0:
                    dp[i % 2][j] = min(dp[i % 2][j], dp[(i - 1) % 2][j - 1] + A[i][j])
                if j + 1 < len(A[0]):
                    dp[i % 2][j] = min(dp[i % 2][j], dp[(i - 1) % 2][j + 1] + A[i][j]) 
        
        # answer
        return min(dp[(n - 1) % 2])
[[java]]
public class Solution {
    /**
     * @param A: the given array
     * @return: the minimum sum of a falling path
     */
    public int minFallingPathSum(int[][] A) {
        int n = A.length, m = A[0].length;
        // state: dp[i][j] 表示从第一行走到 i,j 这个位置的最小路径和
        int[][] dp = new int[2][m];
        
        // initialization: dp[0][i] = A[0][i]
        for (int i = 0; i < m; i++) {
            dp[0][i] = A[0][i];
        }
        
        // function: dp[i][j] = min(dp[i - 1][j - 1], dp[i - 1][j], dp[i - 1][j + 1]) + A[i][j]
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < m; j++) {
                dp[i % 2][j] = dp[(i - 1) % 2][j] + A[i][j];
                if (j - 1 >= 0) {
                    dp[i % 2][j] = Math.min(dp[i % 2][j], dp[(i - 1) % 2][j - 1] + A[i][j]);
                }
                    
                if (j + 1 < A[0].length) {
                    dp[i % 2][j] = Math.min(dp[i % 2][j], dp[(i - 1) % 2][j + 1] + A[i][j]);
                }
            }
        }
            
        // answer
        int answer = Integer.MAX_VALUE;
        for (int i = 0; i < m; i++) {
            answer = Math.min(answer, dp[(n - 1) % 2][i]);
        }
        return answer;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)