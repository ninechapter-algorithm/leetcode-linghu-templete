# 停在原地的方案数2
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/number-of-ways-to-stay-in-the-same-place-after-some-steps-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 有一个长度为 $arrLen$ 的数组，开始有一个指针在索引 $0$ 处。

每一步操作中，你可以将指针向左或向右移动 $1$ 步，或者停在原地（指针不能被移动到数组范围外）。

给你两个整数 $steps$ 和 $arrLen$ ，请你计算并返回：在恰好执行 $steps$ 次操作以后，指针仍然指向索引 $0$ 处的方案数。

由于答案可能会很大，请返回方案数 **模** $10^9 + 7$ 后的结果。


 ### 样例说明
 **样例 1：**

```
输入：
3
2
输出：4
说明：3 步后，总共有 4 种不同的方法可以停在索引 0 处。
向右，向左，不动
不动，向右，向左
向右，不动，向左
不动，不动，不动
```

**样例 2：**

```
输入：
2
4
输出：2
说明：2 步后，总共有 2 种不同的方法可以停在索引 0 处。
向右，向左
不动，不动
```

**样例 3：**

```
输入：
4
2
输出：8
```
 ### 参考代码
 ```
[[python]]
MOD = 10 ** 9 + 7
        

class Solution:
    """
    @param steps: steps you can move
    @param arrLen: the length of the array
    @return: Number of Ways to Stay in the Same Place After Some Steps
    """
    def numWays(self, steps, arrLen):
        # corner case handling
        if arrLen == 1:
            return 1

        # 计算可以走到的最远 index
        n = min(steps // 2 + 1, arrLen)
        
        # state: dp[step][index] 表示走了 step 步以后，停留在 index 位置的方案数
        dp = [[0] * n, [0] * n]
        
        # initialization: 一开始站在 index=0 所以 dp[0][0] = 1
        dp[0][0] = 1
        
        # function:
        # dp[step][index] = dp[step - 1][index - 1] + dp[step - 1][index] + 
        #                   dp[step - 1][index + 1]
        for step in range(1, steps + 1):
            dp[step % 2][0] = (dp[(step - 1) % 2][0] + dp[(step - 1) % 2][1]) % MOD
            dp[step % 2][n - 1] = (dp[(step - 1) % 2][n - 1] + dp[(step - 1) % 2][n - 2]) % MOD
            for index in range(1, n - 1):
                dp[step % 2][index] = sum([
                    dp[(step - 1) % 2][index - 1],
                    dp[(step - 1) % 2][index],
                    dp[(step - 1) % 2][index + 1],
                ]) % MOD
        
        # answer: 走了 steps 步之后，依然停留在 0 这个位置的方案数
        return dp[steps % 2][0]
[[java]]
public class Solution {
    /**
     * @param steps: steps you can move
     * @param arrLen: the length of the array
     * @return: Number of Ways to Stay in the Same Place After Some Steps
     */
    private int MOD = 1000000007; 
    
    public int numWays(int steps, int arrLen) {
        // corner case handling
        if (arrLen == 1) {
            return 1;
        }
        
        // 计算可以走到的最远 index
        int n = Math.min(steps / 2 + 1, arrLen);
        
        // state: dp[step][index] 表示走了 step 步以后，停留在 index 位置的方案数
        int[][] dp = new int[2][n];
        
        // initialization: 一开始站在 index=0 所以 dp[0][0] = 1
        dp[0][0] = 1;
        
        // function:
        // dp[step][index] = dp[step - 1][index - 1] + dp[step - 1][index] + 
        //                   dp[step - 1][index + 1]
        for (int step = 1; step <= steps; step++) {
            dp[step % 2][0] = (dp[(step - 1) % 2][0] + dp[(step - 1) % 2][1]) % MOD;
            dp[step % 2][n - 1] = (dp[(step - 1) % 2][n - 1] + dp[(step - 1) % 2][n - 2]) % MOD;
            for (int index = 1; index < n - 1; index++) {
                dp[step % 2][index] = (int)((
                    1L * dp[(step - 1) % 2][index - 1] +
                    1L * dp[(step - 1) % 2][index] +
                    1L * dp[(step - 1) % 2][index + 1]
                ) % MOD);
            }
        }
        
        // answer: 走了 steps 步之后，依然停留在 0 这个位置的方案数
        return dp[steps % 2][0];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)