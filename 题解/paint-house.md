# 房屋染色
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/paint-house/?utm_source=sc-github-wzz)
 ## 题目描述
 这里有`n`个房子在一列直线上，现在我们需要给房屋染色，分别有红色蓝色和绿色。每个房屋染不同的颜色费用也不同，你需要设计一种染色方案使得**相邻的房屋颜色不同**，并且费用最小，返回最小的费用。

费用通过一个`n`x`3` 的矩阵给出，比如`cost[0][0]`表示房屋`0`染红色的费用，`cost[1][2]`表示房屋`1`染绿色的费用。
 ### 样例说明
 **样例 1:**

```
输入: [[14,2,11],[11,14,5],[14,3,10]]
输出: 10
解释: 第一个屋子染蓝色，第二个染绿色，第三个染蓝色，最小花费：2 + 5 + 3 = 10.
```

**样例 2:**

```
输入: [[1,2,3],[1,4,6]]
输出: 3
```
 ### 参考代码
 动态规划. 

设定状态: f[i][j] 表示第i所房屋涂色为j时, 前i所房屋的最小花费

状态转移方程: f[i][j] = min{f[i-1][k]} +costs[i][j] (k != j)

边界: f[0][i] = costs[0][i]

答案: min{f[n-1][i]} i = 0, 1, 2

优化: 由于状态 f[i][j] 只受 f[i-1][k] 的影响, 所以可以使用滚动数组把空间复杂度降低至 O(1)
```java
public class Solution {
    /**
     * @param costs n x 3 cost matrix
     * @return an integer, the minimum cost to paint all houses
     */
    public int minCost(int[][] costs) {
        int n = costs.length;
        if (n == 0) {
            return 0;
        }
        int[][] f = new int[2][3];
        int old, now = 0;
        f[now][0] = f[now][1] = f[now][2] = 0;
        
        int i, j, k;
        for (i = 1; i <= n; ++i) {
            old = now;
            now = 1 - now;
            for (j = 0; j < 3; ++j) {
                f[now][j] = Integer.MAX_VALUE;
                for (k = 0; k < 3; ++k) {
                    if (k != j && f[old][k] + costs[i-1][j] < f[now][j]) {
                        f[now][j] = f[old][k] + costs[i-1][j];
                    }
                }
            }
        }
        
        int res = f[now][0];
        if (f[now][1] < res) {
            res = f[now][1];
        }
        
        if (f[now][2] < res) {
            res = f[now][2];
        }
        
        return res;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)