# 硬币排成线 III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/coins-in-a-line-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 有 `n` 个硬币排成一条线, 第 `i` 枚硬币的价值为 `values[i]`. 

两个参赛者轮流从任意一边取一枚硬币, 直到没有硬币为止. 拿到硬币总价值更高的获胜.

请判定 **第一个玩家** 会赢还是会输.
 ### 样例说明
 **样例 1:**

```
输入: [3, 2, 2]
输出: true
解释: 第一个玩家在刚开始的时候拿走 3, 然后两个人分别拿到一枚 2.
```

**样例 2:**

```
输入: [1, 20, 4]
输出: false
解释: 无论第一个玩家在第一轮拿走 1 还是 4, 第二个玩家都可以拿到 20.
```
 ### 参考代码
 区间动态规划问题, 具体定义状态的方式有很多种, 但是大同小异, 时空复杂度都相似. 这里只介绍 version 1 的具体实现.

设定 dp[i][j] 表示当前剩余硬币的区间为 [i, j] 时, 此时该拿硬币的人能获取的最大值. 

注意, dp[i][j] 并没有包含角色信息, dp[0][values.length - 1] 表示的是先手的人能获得的最大值, 而 dp[1][values.length -1] 表示的则是后手的人能获得的最大值. 需要这样做是因为: 两个人都会采用最优策略.

当前的人的决策就是拿左边还是拿右边, 而下一个人仍然会最优决策, 所以应该是最小值中取最大值:

```C++
dp[i][j] = max(	                                     // 取max表示当前的人选用最优策略		
    min(dp[i + 2][j], dp[i + 1][j - 1]) + values[i], // 取min表示下一个人选用最优策略
    min(dp[i][j - 2], dp[i + 1][j - 1]) + values[j]
)
```

几个边界:

```
i > j : dp[i][j] = 0
i == j : dp[i][j] = values[i]
i + 1 == j : dp[i][j] = max(values[i], values[j])
```
```java
// version 1
public class Solution {
    /**
     * @param values: an array of integers
     * @return: a boolean which equals to true if the first player will win
     */
    public boolean firstWillWin(int[] values) {
        // write your code here
        int n = values.length;
        int[][] dp = new int[n + 1][n + 1];
        boolean[][] flag = new boolean[n + 1][n + 1];

        int sum = 0;
        for (int now : values)
            sum += now;

        return sum < 2 * MemorySearch(0, values.length - 1, dp, flag, values);
    }

    int MemorySearch(int left, int right, int[][] dp, boolean[][] flag, int[] values) {

        if (flag[left][right])
            return dp[left][right];
        flag[left][right] = true;
        if (left > right) {
            dp[left][right] = 0;
        } else if (left == right) {
            dp[left][right] = values[left];
        } else if (left + 1 == right) {
            dp[left][right] = Math.max(values[left], values[right]);
        } else {
            int pick_left = Math.min(MemorySearch(left + 2, right, dp, flag, values),
                    MemorySearch(left + 1, right - 1, dp, flag, values)) + values[left];
            int pick_right = Math.min(MemorySearch(left, right - 2, dp, flag, values),
                    MemorySearch(left + 1, right - 1, dp, flag, values)) + values[right];
            dp[left][right] = Math.max(pick_left, pick_right);
        }
        return dp[left][right];
    }
}

// version 2
public class Solution {
    /**
     * @param values: an array of integers
     * @return: a boolean which equals to true if the first player will win
     */
    public boolean firstWillWin(int[] values) {
        int n = values.length;
        int[][] dp = new int[n + 1][n + 1];
        boolean[][] flag = new boolean[n + 1][n + 1];
        int[][] sum = new int[n + 1][n + 1];
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                sum[i][j] = i == j ? values[j] : sum[i][j - 1] + values[j];
            }
        }
        int allsum = 0;
        for (int now : values)
            allsum += now;

        return allsum < 2 * MemorySearch(0, values.length - 1, dp, flag, values, sum);
    }

    int MemorySearch(int left, int right, int[][] dp, boolean[][] flag, int[] values, int[][] sum) {
        if (flag[left][right])
            return dp[left][right];

        flag[left][right] = true;
        if (left > right) {
            dp[left][right] = 0;
        } else if (left == right) {
            dp[left][right] = values[left];
        } else if (left + 1 == right) {
            dp[left][right] = Math.max(values[left], values[right]);
        } else {
            int cur = Math.min(MemorySearch(left + 1, right, dp, flag, values, sum),
                    MemorySearch(left, right - 1, dp, flag, values, sum));
            dp[left][right] = sum[left][right] - cur;
        }
        return dp[left][right];
    }
}

// 九章动态规划专题班和算法强化班版本
public class Solution {
    /**
     * @param values: an array of integers
     * @return: a boolean which equals to true if the first player will win
     */
    public boolean firstWillWin(int[] A) {
        // write your code here

        int n = A.length;
        if (n == 0) {
            return true;
        }

        int[][] f = new int[n][n];
        int i, j, len;
        // len 1
        for (i = 0; i < n; ++i) {
            f[i][i] = A[i];
        }

        for (len = 2; len <= n; ++len) {
            for (i = 0; i <= n - len; ++i) {
                j = i + len - 1;
                f[i][j] = Math.max(A[i] - f[i + 1][j], A[j] - f[i][j - 1]);
            }
        }

        return f[0][n - 1] >= 0;
    }
}

// Linpz verision
public class Solution {
    /**
     * @param values: an array of integers
     * @return: a boolean which equals to true if the first player will win
     */
    public boolean firstWillWin(int[] values) {
        int n = values.length;
        int[] sum = new int[n + 1];
        sum[0] = 0;
        for (int i = 1; i <= n; ++i)
            sum[i] = sum[i - 1] + values[i - 1];

        // s[i][j] = sum[j + 1] - sum[i];

        int[][] dp = new int[n][n];
        for (int i = 0; i < n; ++i)
            dp[i][i] = values[i];

        for (int len = 2; len <= n; ++len) {
            for (int i = 0; i < n; ++i) {
                int j = i + len - 1;
                if (j >= n)
                    continue;
                int s = sum[j + 1] - sum[i];
                dp[i][j] = Math.max(s - dp[i + 1][j], s - dp[i][j - 1]);
            }
        }

        return dp[0][n - 1] > sum[n] / 2;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)