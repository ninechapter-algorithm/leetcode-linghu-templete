# 爬楼梯 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/climbing-stairs-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 一个小孩爬一个 n 层台阶的楼梯。他可以每次跳 1 步， 2 步 或者 3 步。实现一个方法来统计总共有多少种不同的方式爬到最顶层的台阶。

 ### 样例说明
 
 ### 参考代码
 本题采用动态规划的思想，每一步的答案可以由上三步转移而来。
初始状态和状态转移方程如下：
$f_0=1,\ f_1 =1,\ f_2=2,f_n=f_{n-1}+f_{n-2}+f_{n-3}(n \geq 3)$
```java
public class Solution {
    /**
     * @param n an integer
     * @return an integer
     */
    public int climbStairs2(int n) {
        int[] f = new int[n+1];
        f[0] = 1;
        for (int i = 0; i <= n; i++) 
            for (int j = 1; j <= 3; j++) {
                if (i >= j) {
                    f[i] += f[i-j];
                }
            }
        return f[n];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)