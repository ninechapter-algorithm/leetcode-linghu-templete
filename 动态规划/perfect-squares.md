# 完美平方
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/perfect-squares/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个正整数 n, 请问最少多少个完全平方数(比如1, 4, 9...)的和等于n。


 ### 样例说明
 **样例 1:**

```
输入: 12
输出: 3
解释: 4 + 4 + 4
```

**样例 2:**

```
输入: 13
输出: 2
解释: 4 + 9
```
 ### 参考代码
 # 做法1:
## 算法：dp
我们用f[i]表示i最少能被几个完全平方数来表示。
- 首先我们对dp数组赋予初值，对于每个完全平方数的f=1。
- 利用记忆化搜索来完成查找。对于i，我们考虑i的前继状态，也就是哪几个状态可以加上一个完全平方数抵达i。
- 对于所有能够抵达i的状态，取他们的最小值+1即可。

上述过程的状态转移方程为 f[i] = min{f[i], f\[i - j \* j] + 1} (j\*j <= i)

边界: f\[i\*i] = 1

## 复杂度分析
* 时间复杂度`O(n)`
  * 枚举了数组的长度
* 空间复杂度`O(n^(3/2))`
  * 对于每个数，它的前继状态都有sqrt(i)个，i为这个数的大小。
  * 所以总的复杂度为sqrt(1)+sqrt(2)+....sqrt(n)约等于O(n^(3/2))
  * 证明过程太复杂，就不在此给出。
    

---

# 做法2:
##算法：数学做法
涉及[四平方和定理](https://zh.wikipedia.org/wiki/%E5%9B%9B%E5%B9%B3%E6%96%B9%E5%92%8C%E5%AE%9A%E7%90%86)
参考 <http://www.cnblogs.com/grandyang/p/4800552.html>
根据四平方和定理，我们可以发现，一个数能被四个数之内的平方和表示。
* 我们直接循环，判断这个数能否被1~到3个数的平方和表示即可，若不行，直接输出4

## 复杂度分析
* 时间复杂度`O(n)`
  * 两重循环的上限为sqrt(n)，相乘即可。
* 空间复杂度`O(1)`
  * 消耗了常数的空间
```java
///////////////// version 0 DP
public class Solution {
    /**
     * @param n a positive integer
     * @return an integer
     */
    public int numSquares(int n) {
        // Write your code here
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        for (int i = 0; i * i <= n; ++i) {
            dp[i * i] = 1;
        }

        for (int i = 0; i <= n; ++i) {
            for (int j = 1; j * j <= i; ++j) {
                dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
            }
        }

        return dp[n];
    }
}

////////////////// version 1 DP 
public class Solution {
    /**
     * @param n a positive integer
     * @return an integer
     */
    public int numSquares(int n) {
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        for(int i = 0; i * i <= n; ++i)
            dp[i * i] = 1;

        for (int i = 0; i <= n; ++i)
            for (int j = 0; i + j * j <= n; ++j)
                dp[i + j * j] = Math.min(dp[i] + 1, dp[i + j * j]);

        return dp[n];
    }
}

//////////////// version 2  Math
public class Solution {
    /**
     * @param n a positive integer
     * @return an integer
     */
    public int numSquares(int n) {
        while (n % 4 == 0)
            n /= 4;
        if (n % 8 == 7)
            return 4;
        for (int i = 0; i * i <= n; ++i) {
            int j = (int)Math.sqrt(n * 1.0 - i * i);
            if (i * i + j * j == n) {
                int res = 0;
                if (i > 0)
                    res += 1;
                if (j > 0)
                    res += 1;
                return res;
            }
        }
        return 3;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)