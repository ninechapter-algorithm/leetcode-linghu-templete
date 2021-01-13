# 爬楼梯
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/climbing-stairs/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>假设你正在爬楼梯，需要n步你才能到达顶部。但每次你只能爬一步或者两步，你能有多少种不同的方法爬到楼顶部？</p>
 ### 样例说明
 
 ### 参考代码
 You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

考虑最后一步走1阶还是走2阶。
方案数Dp[n] = 最后一步走1阶的方案数 + 最后一步走2阶的方案数。
Dp[n] = Dp[n-1] + Dp[n-2].
```java
public class Solution {
    public int climbStairs(int n) {
        if (n <= 1) {
            return n;
        }
        int last = 1, lastlast = 1;
        int now = 0;
        for (int i = 2; i <= n; i++) {
            now = last + lastlast;
            lastlast = last;
            last = now;
        }
        return now;
    }
}

// 记忆化搜索
// 九章硅谷求职算法集训营版本
public class Solution {
    /**
     * @param n: An integer
     * @return: An integer
     */
    int[] result = null;

    void f(int X) {
         if (result[X] != -1) return;                                                 
         if (X == 0 || X == 1) {
            result[X] = 1;
            return;
         }
         
         f(X - 1);
         f(X - 2);
         result[X] = result[X - 1] + result[X - 2];
    }

    public int climbStairs(int n) {
        if (n == 0) {
            return 0;
        }
        
        result  = new int[n + 1];
        for (int i = 0; i <= n; ++i) {
            result[i] = -1;
        }
        
        f(n);
        return result[n];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)