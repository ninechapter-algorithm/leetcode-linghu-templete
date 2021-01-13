# 凑 N 分钱的方案数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/number-of-ways-to-represent-n-cents/?utm_source=sc-github-wzz)
 ## 题目描述
 给你无限多个的 25 分，10 分，5 分和 1 分的硬币。问如果要凑出 `n` 分钱有多少种不同的方式？
 ### 样例说明
 **样例 1:**
```
输入:n = `11`
输出: 4
解释:
11 = 1 + 1 + 1... + 1
     = 1 + 1 + 1 + 1 + 1 + 1 + 5
     = 1 + 5 + 5
     = 1 + 10
```

**样例 2:**
```
输入:n = `9`
输出: 2
解释:
9 = 1 + 1 + 1... + 1
   = 1 + 1 + 1 + 1  + 5
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param n an integer
     * @return an integer
     */
    public int waysNCents(int n) {
        int[] f = new int[n+1];
        f[0] = 1;
        int[] cents = new int[]{1, 5, 10, 25};
        for (int i = 0; i < 4; i++) 
            for (int j = 1; j <= n; j++) {
                if (j >= cents[i]) {
                    f[j] += f[j-cents[i]];
                }
            }
        return f[n];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)