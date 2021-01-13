# 栅栏染色
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/paint-fence/?utm_source=sc-github-wzz)
 ## 题目描述
 我们有一个栅栏，它有`n`个柱子，现在要给柱子染色，有`k`种颜色可以染。
必须保证不存在超过2个相邻的柱子颜色相同，求有多少种染色方案。
 ### 样例说明
 例 1:
```
输入: n=3, k=2  
输出: 6
Explanation:
          post 1,   post 2, post 3
    way1    0         0       1 
    way2    0         1       0
    way3    0         1       1
    way4    1         0       0
    way5    1         0       1
    way6    1         1       0
```

例 2:
```
输入: n=2, k=2  
输出: 4
Explanation:
          post 1,   post 2
    way1    0         0       
    way2    0         1            
    way3    1         0          
    way4    1         1       
```

 ### 参考代码
 采用动态规划的思想。
dp[i]=(k-1)×(dp[i-1]+dp[i-2]) 
dp[i-1]×(k-1)代表当前格子的颜色和前一个不同的方案
dp[i-2]×(k-1)代表当前格子的颜色和前一个相同的方案
```java
public class Solution {
    /**
     * @param n non-negative integer, n posts
     * @param k non-negative integer, k colors
     * @return an integer, the total number of ways
     */
    public int numWays(int n, int k) {
        // Write your code here
        int dp[] = {0, k , k*k, 0};
        if(n <= 2)
            return dp[n];
        if (k == 1)
            return 0;
        for(int i = 2; i < n; i++) {
            dp[3] = (k - 1) * (dp[1] + dp[2]);
            dp[1] = dp[2];
            dp[2] = dp[3];
        }
        return dp[3];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)