# 合并石头的最低成本
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-cost-to-merge-stones/?utm_source=sc-github-wzz)
 ## 题目描述
 有 N 堆石头排成一排，第 i 堆中有 stones[i] 块石头。

每次移动（move）需要将连续的 K 堆石头合并为一堆，而这个移动的成本为这 K 堆石头的总数。

找出把所有石头合并成一堆的最低成本。如果不可能，返回 -1 。
 ### 样例说明
 示例 1：
```
输入：stones = [3,2,4,1], K = 2
输出：20
解释：
从 [3, 2, 4, 1] 开始。
合并 [3, 2]，成本为 5，剩下 [5, 4, 1]。
合并 [4, 1]，成本为 5，剩下 [5, 5]。
合并 [5, 5]，成本为 10，剩下 [10]。
总成本 20，这是可能的最小值。
```
示例 2：
```
输入：stones = [3,2,4,1], K = 3
输出：-1
解释：任何合并操作后，都会剩下 2 堆，我们无法再进行合并。所以这项任务是不可能完成的。
```
 ### 参考代码
 用记忆化搜索实现的 DP。
`dp[i][j][k]` 代表从 i 合并到 j，最后剩下 k 堆的最小耗费。
最后答案是 `dp[0][n - 1][1]`。特别的，`dp[i][j][1] = dp[i][j][k] + sum[i][j]`
```java
class Solution {
    public int mergeStones(int[] stones, int K) {
        int n = stones.length;
        int[][][] memo = new int[n][n][K + 1];
        int[][] rangeSum = getRangeSum(stones);
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                for (int k = 1; k <= K; k++) {
                    memo[i][j][k] = Integer.MAX_VALUE;
                }
            }
        }
        return memoSearch(rangeSum, 0, n - 1, 1, K, memo);
    }
    
    private int memoSearch(int[][] rangeSum, int left, int right, int k, int K, int[][][] memo) {
        if (memo[left][right][k] != Integer.MAX_VALUE) {
            return memo[left][right][k];
        }
        
        if (left == right) {
            if (k == 1) {
                return 0;
            }
            return -1;
        }
        
        if (k == 1) {
            int result = memoSearch(rangeSum, left, right, K, K, memo);
            if (result == -1) {
                return -1;
            }
            return result + rangeSum[left][right];
        }
        
        int minimum = Integer.MAX_VALUE;
        for (int i = left; i <= right - k + 1; i++) {
            int first_part = memoSearch(rangeSum, left, i, 1, K, memo);
            int rest_parts = memoSearch(rangeSum, i + 1, right, k - 1, K, memo);
            if (first_part == -1 || rest_parts == -1) {
                continue;
            }
            minimum = Math.min(minimum, first_part + rest_parts);
        }
        
        if (minimum == Integer.MAX_VALUE) {
            minimum = -1;
        }
        memo[left][right][k] = minimum;
        return minimum;
    }
    
    private int[][] getRangeSum(int[] stones) {
        int[][] rangeSum = new int[stones.length][stones.length];
        
        for (int i = 0; i < stones.length; i++) {
            rangeSum[i][i] = stones[i];
        }
        
        for (int i = stones.length - 1; i >= 0; i--) {
            for (int j = i + 1; j < stones.length; j++) {
                rangeSum[i][j] = rangeSum[i][j - 1] + stones[j];
            }
        }

        return rangeSum;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)