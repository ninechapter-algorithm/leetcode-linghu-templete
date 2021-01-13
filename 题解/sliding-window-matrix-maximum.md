# 滑动窗口矩阵的最大值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sliding-window-matrix-maximum/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个 `n * m` 的一个矩阵, 以及一个移动的矩阵窗口 (大小为 `k * k`), 移动窗口从左上角到右下角, 找到每一次移动窗口得到的和中的最大值, 返回 `0`, 如果结果不存在 
 ### 样例说明
 **样例 1:**
```
输入：[[1,5,3],[3,2,1],[4,1,9]]，k=2
输出：13
解释：
最初窗口位于矩阵的起点如下
	[
	  [|1, 5|, 3],
	  [|3, 2|, 1],
	  [4, 1, 9],
	]
,得到和为 11;

然后窗口向前移动一步
	[
	  [1, |5, 3|],
	  [3, |2, 1|],
	  [4, 1, 9],
	]
,得到和为 11;

然后窗口继续移动一步
	[
	  [1, 5, 3],
	  [|3, 2|, 1],
	  [|4, 1|, 9],
	]
,得到和为 10;

然后窗口继续移动一步
	[
	  [1, 5, 3],
	  [3, |2, 1|],
	  [4, |1, 9|],
	]
,得到和为 13;
所以最终，从所有窗口中得到最大值为13。
```

**样例 2:**
```
输入：[[10]，k=1
输出：10
解释：
滑动窗口的大小为 1*1，返回 10。
```

 ### 参考代码
 考点：
* 二维前缀和

题解：
* sum[i][j]存储左上角坐标为(0,0),右下角坐标为(i,j)的子矩阵的和。
* sum[i][j] = matrix[i - 1][j - 1] + sum[i - 1][j] + sum[i][j - 1] - sum[i - 1][j - 1];递推求值即可，两部分相加，减去重复计算部分。
* int value = sum[i][j] - sum[i - k][j] -sum[i][j - k] + sum[i - k][j - k];可求得一个k * k大小子矩阵的和。
```java
public class Solution {
    /**
     * @param matrix an integer array of n * m matrix
     * @param k an integer
     * @return the maximum number
     */
    public int maxSlidingWindow2(int[][] matrix, int k) {
        // Write your code here
        int n = matrix.length;
        if (n == 0 || n < k)
            return 0;
        int m = matrix[0].length;
        if (m == 0 || m < k)
            return 0;

        int[][] sum = new int[n + 1][m + 1];
        for (int i = 0; i <= n; ++i) sum[i][0] = 0;
        for (int i = 0; i <= m; ++i) sum[0][i] = 0;

        for (int i = 1; i <= n; ++i)
            for (int j = 1; j <= m; ++j)
                sum[i][j] = matrix[i - 1][j - 1] + 
                            sum[i - 1][j] + sum[i][j - 1] - sum[i - 1][j - 1];

        int max_value = Integer.MIN_VALUE;
        for (int i = k; i <= n; ++i)
            for (int j = k; j <= m; ++j) {
                int value = sum[i][j] - sum[i - k][j] -
                            sum[i][j - k] + sum[i - k][j - k];

                if (value > max_value)
                    max_value = value;
            }
        return max_value;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)