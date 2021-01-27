# 老鼠跳跃
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/rat-jump/?utm_source=sc-github-wzz)
 ## 题目描述
 有一个老鼠从高为`n`的楼梯顶部跳跃下来，这个老鼠在偶数次跳跃时可以跳1, 3或者4个台阶，奇数次可以跳跃1, 2或者4个台阶。但是楼梯中间会有一些台阶上有胶水，如果跳到那些台阶上，老鼠就会被直接粘住，无法继续跳跃。你需要求出从这个楼梯顶部开始，老鼠有多少种方法能够到达地面，即第0层。若超过地面，也算是可以到达。例如从1跳跃到-1，和从1跳跃到0的方案不同。楼梯有无胶水的状态是从高往低输入的，即arr[0]代表当前老鼠所在的位置无胶水。
 ### 样例说明
 
 ### 参考代码
 ```
[[python]]
MOD = 10 ** 9 + 7


class Solution:
    """
    @param arr: the steps whether have glue
    @return: the sum of the answers
    """
    def ratJump(self, arr):
        n = len(arr)

        # state: dp[i][0] 代表从 0 的位置跳偶数步后到 i 的位置的方案数
        #        dp[i][1] 代表从 0 的位置跳奇数步后到 i 的位置的方案数
        dp = [[0, 0] for _ in range(n)]
        
        # initialization: 一开始站在 0 的位置, 已经跳过了 0 步(偶数步)
        dp[0][0] = 1
        
        even_jumps = [1, 3, 4]
        odd_jumps = [1, 2, 4]
        
        # function: dp[i][0] = dp[i - 1][1] + dp[i - 3][1] + dp[i - 4][1]
        #           dp[i][1] = dp[i - 1][0] + dp[i - 2][0] + dp[i - 4][0]
        for i in range(1, n - 1):
            if arr[i] == 1:
                continue
            for jump in even_jumps:
                if i - jump >= 0:
                    dp[i][0] = (dp[i][0] + dp[i - jump][1]) % MOD
            for jump in odd_jumps:
                if i - jump >= 0:
                    dp[i][1] = (dp[i][1] + dp[i - jump][0]) % MOD
        
        # answer: 研究跳到地板之前的那一步是从哪儿出发的，跳了多远
        plans = 0
        for jump in even_jumps:
            for i in range(max(0, n - jump - 1), n - 1):
                plans = (plans + dp[i][1]) % MOD
        for jump in odd_jumps:
            for i in range(max(0, n - jump - 1), n - 1):
                plans = (plans + dp[i][0]) % MOD
        return plans
[[java]]
public class Solution {
    /**
     * @param arr: the steps whether have glue
     * @return: the sum of the answers
     */
    private int MOD = 1000000007; 
    
    public int ratJump(int[] arr) {
        int n = arr.length;

        // state: dp[i][0] 代表从 0 的位置跳偶数步后到 i 的位置的方案数
        //        dp[i][1] 代表从 0 的位置跳奇数步后到 i 的位置的方案数
        int[][] dp = new int[n][2];
        
        // initialization: 一开始站在 0 的位置, 已经跳过了 0 步(偶数步)
        dp[0][0] = 1;
        
        int[] evenJumps = {1, 3, 4};
        int[] oddJumps = {1, 2, 4};
        
        // function: dp[i][0] = dp[i - 1][1] + dp[i - 3][1] + dp[i - 4][1]
        //           dp[i][1] = dp[i - 1][0] + dp[i - 2][0] + dp[i - 4][0]
        for (int i = 1; i < n - 1; i++) {
            if (arr[i] == 1) {
                continue;
            }
            for (int jump: evenJumps) {
                if (i - jump >= 0) {
                    dp[i][0] = (dp[i][0] + dp[i - jump][1]) % MOD;
                }
            }
                
            for (int jump: oddJumps) {
                if (i - jump >= 0) {
                    dp[i][1] = (dp[i][1] + dp[i - jump][0]) % MOD;
                }
            }
        }
            
        
        // answer: 研究跳到地板之前的那一步是从哪儿出发的，跳了多远
        int plans = 0;
        for (int jump: evenJumps) {
            for (int i = Math.max(0, n - jump - 1); i < n - 1; i++) {
                plans = (plans + dp[i][1]) % MOD;
            }
        }
            
        for (int jump: oddJumps) {
            for (int i = Math.max(0, n - jump - 1); i < n - 1; i++) {
                plans = (plans + dp[i][0]) % MOD;
            }
        }
        return plans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)