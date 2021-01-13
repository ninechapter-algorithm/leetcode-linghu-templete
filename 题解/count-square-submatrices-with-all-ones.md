# 统计全为 1 的正方形子矩阵
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/count-square-submatrices-with-all-ones/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个 m * n 的矩阵，矩阵中的元素不是 0 就是 1，请你统计并返回其中完全由 1 组成的 正方形 子矩阵的个数。
 ### 样例说明
 
 ### 参考代码
 ```
[[python]]
class Solution:
    """
    @param matrix: a matrix
    @return: return how many square submatrices have all ones
    """
    def countSquares(self, matrix):
        n, m = len(matrix), len(matrix[0])
        
        # state: dp[i][j] 表示以 i,j 作为右下角的全1正方形有多少个(最大是多少)
        # state: left[i][j] 表示 i,j 往左连续的 1 最长多长
        # state: up[i][j] 表示 i,j 往上连续的 1 最长多长
        dp = [[0] * m for _ in range(n)]
        left = [[0] * m for _ in range(n)]
        up = [[0] * m for _ in range(n)]
        
        # initialization: 初始化第一行和第一列
        for i in range(n):
            dp[i][0] = left[i][0] = up[i][0] = matrix[i][0]
        for j in range(m):
            dp[0][j] = left[0][j] = up[0][j] = matrix[0][j]
        
        # function: 如果 matrix[i][j] == 0 那么 dp[i][j] = 0 否则
        #   dp[i][j] = min(left[i][j - 1], up[i - 1][j], dp[i - 1][j - 1]) + 1
        #   也可以写作
        #   dp[i][j] = min(left[i][j], up[i][j], dp[i - 1][j - 1] + 1)
        for i in range(1, n):
            for j in range(1, m):
                if matrix[i][j] == 0:
                    continue
                left[i][j] = left[i][j - 1] + 1
                up[i][j] = up[i - 1][j] + 1
                dp[i][j] = min(left[i][j - 1], up[i - 1][j], dp[i - 1][j - 1]) + 1
        
        # answer: 统计每个位置作为右下角的矩阵有多少个，加起来
        answer = 0
        for i in range(n):
            answer += sum(dp[i])
        return answer
[[java]]
public class Solution {
    /**
     * @param matrix: a matrix
     * @return: return how many square submatrices have all ones
     */
    public int countSquares(int[][] matrix) {
        int n = matrix.length, m = matrix[0].length;
        
        // state: dp[i][j] 表示以 i,j 作为右下角的全1正方形有多少个(最大是多少)
        // state: left[i][j] 表示 i,j 往左连续的 1 最长多长
        // state: up[i][j] 表示 i,j 往上连续的 1 最长多长
        int[][] dp = new int[n][m];
        int[][] left = new int[n][m];
        int[][] up = new int[n][m];
        
        // initialization: 初始化第一行和第一列
        for (int i = 0; i < n; i++) {
            dp[i][0] = left[i][0] = up[i][0] = matrix[i][0];
        }
        for (int j = 0; j < m; j++) {
            dp[0][j] = left[0][j] = up[0][j] = matrix[0][j];
        }
        
        // function: 如果 matrix[i][j] == 0 那么 dp[i][j] = 0 否则
        //   dp[i][j] = min(left[i][j - 1], up[i - 1][j], dp[i - 1][j - 1]) + 1
        //   也可以写作
        //   dp[i][j] = min(left[i][j], up[i][j], dp[i - 1][j - 1] + 1)
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                if (matrix[i][j] == 0) {
                    continue;
                }
                left[i][j] = left[i][j - 1] + 1;
                up[i][j] = up[i - 1][j] + 1;
                dp[i][j] = Math.min(Math.min(left[i][j - 1], up[i - 1][j]), dp[i - 1][j - 1]) + 1;
            }
        }
                
        // answer: 统计每个位置作为右下角的矩阵有多少个，加起来
        int answer = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                answer += dp[i][j];
            }
        }
        
        return answer;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)