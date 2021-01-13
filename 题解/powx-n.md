# x的n次幂
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/powx-n/?utm_source=sc-github-wzz)
 ## 题目描述
 实现 pow(x, n). (n是一个整数)
 ### 样例说明
 **样例 1:**

```
输入: x = 9.88023, n = 3
输出: 964.498
```

**样例 2:**

```
输入: x = 2.1, n = 3
输出: 9.261
```

**样例 3:**

```
输入: x = 1, n = 0
输出: 1
```
 ### 参考代码
 注意 n 可能是负数, 需要求一下倒数, 可以在一开始把x转换成倒数, 也可以到最后再把结果转换为倒数.

那么现在我们实现 pow(x, n), n 是正整数的版本:

二分即可: 有 $x^n = x{n/2} * x{n/2}$, 因此可以在 O(*logn*) 的时间复杂度内实现.

又叫快速幂. 有递归实现和循环实现的版本.

*还可以参考一下 fast power 中的[二进制的做法](https://www.jiuzhang.com/solutions/fast-power)。*
```java
public class Solution {
    /**
     * @param x the base number
     * @param n the power number
     * @return the result
     */
    public double myPow(double x, int n) {
        boolean isNegative = false;
        if (n < 0) {
            x = 1 / x;
            isNegative = true;
            n = -(n + 1);       // Avoid overflow when n == MIN_VALUE
        }

        double ans = 1, tmp = x;

        while (n != 0) {
            if (n % 2 == 1) {
                ans *= tmp;
            }
            tmp *= tmp;
            n /= 2;
        }
        
        if (isNegative) {
            ans *= x;
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)