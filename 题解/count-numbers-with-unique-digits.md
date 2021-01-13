# 计算不同数字整数的个数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/count-numbers-with-unique-digits/?utm_source=sc-github-wzz)
 ## 题目描述
 给定**非负**整数n，计算具有不同数字字符的所有整数，其中$0 \leq x \lt 10^n$。
 ### 样例说明
 **样例1**
```
输入： 2
输出： 91
解释：
答案应该是0≤x<100范围内的总数，除去[11,22,33,44,55,66,77,88,99]
```
**样例2**
```
输入： 3
输出： 739
```
 ### 参考代码
 对于dp的做法：
设dp[i]表示i位数时满足题意的数的个数。
对于第i位，为了使得第i位与前i-1位的数字不一致，我们可以选择数字应该有$10-(i-1)$个，因此转移方程为：$dp[i]=dp[i-1]*(11-i)$
```java
//  solution 1
//DP Solution
public class Solution {
    /**
     * @param n: a non-negative integer
     * @return: number of numbers with unique digits
     */
    public int countNumbersWithUniqueDigits(int n) {
        // Write your code here 
        if (n == 0) return 1;
    	//dp[i]表示i位数时UniqueDigits的数量
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 9;
        
        int sum = 10;
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i-1] * (11 - i);
            //i = 2; dp[2] = dp[1] * 9 
            /*
            9表示，在一位数的基础上，添加一个数使他成为一个二位数
            对于每一个一位数的UniqueDigit有9种添加的方法使之成为二位数的UniqueDigit
            */
            sum += dp[i];
        }
        return sum;
    
    }
}

// solution 2
//Math Method
public class Solution {
    public int countNumbersWithUniqueDigits(int n) {
        if (n == 0) {
            return 1;
        }
        if (n > 10) {
            n = 10;
        }
        int ans = 1;
        int multiple = 9;
        for (int i = n - 1; i >= 0; i--) {
            if (i == 0) {
                ans += multiple;
            } else {
                ans += (n - i + 1) * multiple;
            }
            multiple = multiple * (10 - n + i - 1);
        }
        return ans;
    } 
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)