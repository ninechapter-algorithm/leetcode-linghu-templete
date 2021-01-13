# 盈利计划
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/profitable-schemes/?utm_source=sc-github-wzz)
 ## 题目描述
 帮派里有 G 名成员，他们可能犯下各种各样的罪行。

第 `i` 种犯罪会产生 `profit[i]` 的利润，它要求 `group[i]` 名成员共同参与。

让我们把这些犯罪的任何子集称为盈利计划，该计划至少产生 `P` 的利润。

有多少种方案可以选择？因为答案很大，所以返回它模 `10^9 + 7` 的值。
 ### 样例说明
 **示例 1：**
```
输入：G = 5, P = 3, group = [2,2], profit = [2,3]
输出：2
解释： 
至少产生 3 的利润，该帮派可以犯下罪 0 和罪 1 ，或仅犯下罪 1 。
总的来说，有两种方案。
```

**示例 2:**
```
输入：G = 10, P = 5, group = [2,3,5], profit = [6,7,8]
输出：7
解释：
至少产生 5 的利润，只要他们犯其中一种罪就行，所以该帮派可以犯下任何罪行 。
有 7 种可能的计划：(0)，(1)，(2)，(0,1)，(0,2)，(1,2)，以及 (0,1,2) 。
```
 ### 参考代码
 `dp[i][j][k]` 表示前 i 个 crimes 里，用刚好 j 个人，获得至少 k 的盈利，有多少方案的解法
```
[[python]]
class Solution:
    """
    @param G: The people in a gang.
    @param P: A profitable scheme any subset of these crimes that generates at least P profit.
    @param group: The i-th crime requires group[i] gang members to participate.
    @param profit: The i-th crime generates a profit[i].
    @return: Return how many schemes can be chosen.
    """
    def profitableSchemes(self, G, P, group, profit):
        n = len(group)
        
        # state: dp[i][j][k] 前 i 个 crimes 里，用刚好 j 个人，获得至少 k 的盈利，有多少方案
        dp = [
            [
                [0] * (P + 1)
                for _ in range(G + 1)
            ]
            for __ in range(2)
        ]

        # initialization: 前 0 个 crimes 里，用刚好 0 个人，至少获得 0 的盈利，方案数是1
        dp[0][0][0] = 1
            
        # function:
        # dp[i][j][k] = dp[i - 1][j][k] // 不执行 crimes[i - 1] 的情况
        #             + dp[i - 1][j - group[i - 1]][k - profile[i - 1]] // 执行 crimes[i - 1]
        # 当 k - profile[i - 1] < 0 的时候，直接让这个值 = 0
        for i in range(1, n + 1):
            for j in range(G + 1):
                for k in range(P + 1):
                    dp[i % 2][j][k] = dp[(i - 1) % 2][j][k]
                    if j >= group[i - 1]:
                        prev_k = max(k - profit[i - 1], 0)
                        dp[i % 2][j][k] += dp[(i - 1) % 2][j - group[i - 1]][prev_k]
        
        # answer: sum(dp[n][0..G][P]) 把所有不同的人数能够获得的盈利加起来
        total = 0
        for g in range(G + 1):
            total += dp[n % 2][g][P]
        return total
[[java]]
public class Solution {
    /**
     * @param G: The people in a gang.
     * @param P: A profitable scheme any subset of these crimes that generates at least P profit.
     * @param group: The i-th crime requires group[i] gang members to participate.
     * @param profit: The i-th crime generates a profit[i].
     * @return: Return how many schemes can be chosen.
     */
    public int profitableSchemes(int G, int P, int[] group, int[] profit) {
        int n = group.length;
        
        // state: dp[i][j][k] 前 i 个 crimes 里，用刚好 j 个人，获得至少 k 的盈利，有多少方案
        int[][][] dp = new int[2][G + 1][P + 1];
        
        // initialization: 前 0 个 crimes 里，用刚好 0 个人，至少获得 0 的盈利，方案数是1
        dp[0][0][0] = 1;
        
        // function:
        // dp[i][j][k] = dp[i - 1][j][k] // 不执行 crimes[i - 1] 的情况
        //             + dp[i - 1][j - group[i - 1]][k - profile[i - 1]] // 执行 crimes[i - 1]
        // 当 k - profile[i - 1] < 0 的时候，直接让这个值 = 0
        for (int i = 1; i <= n; i++) {
            for (int j = 0; j <= G; j++) {
                for (int k = 0; k <= P; k++) {
                    dp[i % 2][j][k] = dp[(i - 1) % 2][j][k];
                    if (j >= group[i - 1]) {
                        int prevK = Math.max(k - profit[i - 1], 0);
                        dp[i % 2][j][k] += dp[(i - 1) % 2][j - group[i - 1]][prevK];
                    }
                }
            }
        }
           
        // answer: sum(dp[n][0..G][P]) 把所有不同的人数能够获得的盈利加起来
        int total = 0;
        for (int g = 0; g <= G; g++) {
            total += dp[n % 2][g][P];
        }
            
        return total;
    }
}
```
`dp[i][j][k]` 表示前 i 个 crimes 里，用小于等于 j 个人，获得至少 k 的盈利，有多少方案的解法
```
[[python]]
class Solution:
    """
    @param G: The people in a gang.
    @param P: A profitable scheme any subset of these crimes that generates at least P profit.
    @param group: The i-th crime requires group[i] gang members to participate.
    @param profit: The i-th crime generates a profit[i].
    @return: Return how many schemes can be chosen.
    """
    def profitableSchemes(self, G, P, group, profit):
        n = len(group)
        
        # state: dp[i][j][k] 前 i 个 crimes 里，用小于等于 j 个人，获得至少 k 的盈利，有多少方案
        dp = [
            [
                [0] * (P + 1)
                for _ in range(G + 1)
            ]
            for __ in range(2)
        ]

        # initialization: 前 0 个 crimes 里，用小于等于 i 个人，至少获得 0 的盈利，方案数是1
        for i in range(G + 1):
            dp[0][i][0] = 1
            
        # function:
        # dp[i][j][k] = dp[i - 1][j][k] // 不执行 crimes[i - 1] 的情况
        #             + dp[i - 1][j - group[i - 1]][k - profile[i - 1]] // 执行 crimes[i - 1]
        # 当 k - profile[i - 1] < 0 的时候，直接让这个值 = 0
        for i in range(1, n + 1):
            for j in range(G + 1):
                for k in range(P + 1):
                    dp[i % 2][j][k] = dp[(i - 1) % 2][j][k]
                    if j >= group[i - 1]:
                        prev_k = max(k - profit[i - 1], 0)
                        dp[i % 2][j][k] += dp[(i - 1) % 2][j - group[i - 1]][prev_k]
        
        # answer: dp[n][G][P] 前 n 个crimes 里，用小于等于 G 个人，获得至少 P 的盈利，有多少方案
        return dp[n % 2][G][P]
[[java]]
public class Solution {
    /**
     * @param G: The people in a gang.
     * @param P: A profitable scheme any subset of these crimes that generates at least P profit.
     * @param group: The i-th crime requires group[i] gang members to participate.
     * @param profit: The i-th crime generates a profit[i].
     * @return: Return how many schemes can be chosen.
     */
    public int profitableSchemes(int G, int P, int[] group, int[] profit) {
        int n = group.length;
        
        // state: dp[i][j][k] 前 i 个 crimes 里，用刚好 j 个人，获得至少 k 的盈利，有多少方案
        int[][][] dp = new int[2][G + 1][P + 1];
        
        // initialization: 前 0 个 crimes 里，用小于等于 i 个人，至少获得 0 的盈利，方案数是1
        for (int i = 0; i <= G; i++) {
            dp[0][i][0] = 1;
        }
        
        // function:
        // dp[i][j][k] = dp[i - 1][j][k] // 不执行 crimes[i - 1] 的情况
        //             + dp[i - 1][j - group[i - 1]][k - profile[i - 1]] // 执行 crimes[i - 1]
        // 当 k - profile[i - 1] < 0 的时候，直接让这个值 = 0
        for (int i = 1; i <= n; i++) {
            for (int j = 0; j <= G; j++) {
                for (int k = 0; k <= P; k++) {
                    dp[i % 2][j][k] = dp[(i - 1) % 2][j][k];
                    if (j >= group[i - 1]) {
                        int prevK = Math.max(k - profit[i - 1], 0);
                        dp[i % 2][j][k] += dp[(i - 1) % 2][j - group[i - 1]][prevK];
                    }
                }
            }
        }
           
        // answer: dp[n][G][P] 前 n 个crimes 里，用小于等于 G 个人，获得至少 P 的盈利，有多少方案
        return dp[n % 2][G][P];
    }
}


```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)