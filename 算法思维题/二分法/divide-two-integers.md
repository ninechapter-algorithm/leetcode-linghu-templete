# 两个整数相除
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/divide-two-integers/?utm_source=sc-github-wzz)
 ## 题目描述
 将两个整数相除，**要求不使用乘法、除法和 mod 运算符。**

如果溢出(超出32位有符号整型表示范围)，返回 `2147483647` 。

整数除法应截断为零。
 ### 样例说明
 **样例 1:**

```
输入: 被除数 = 0, 除数 = 1
输出: 0
```

**样例 2:**

```
输入: 被除数 = 100, 除数 = 9
输出: 11
```
 ### 参考代码
 基本思路是利用减法, 看看被除数可以减去多少次除数.

使用倍增的思想优化, 可以将减法的次数优化到对数时间复杂度.

我们将除数左移一位(或者让它加上自己), 即得到了二倍的除数, 这时一次减法相当于减去了2个除数. 不断倍增, 时间效率很优秀.

与此同时还需要一个变量记录此时的除数是最初的除数的多少倍, 每次减法后都加到结果上即可.

---

还可参考九章算法微博: <http://weibo.com/3948019741/BtiIg7xm4>
```java
public class Solution {
    /**
     * @param dividend the dividend
     * @param divisor the divisor
     * @return the result
     */
    public int divide(int dividend, int divisor) {
        if (divisor == 0) {
             return dividend >= 0? Integer.MAX_VALUE : Integer.MIN_VALUE;
        }
        
        if (dividend == 0) {
            return 0;
        }
        
        if (dividend == Integer.MIN_VALUE && divisor == -1) {
            return Integer.MAX_VALUE;
        }
        
        boolean isNegative = (dividend < 0 && divisor > 0) || 
                             (dividend > 0 && divisor < 0);
                             
        long a = Math.abs((long)dividend);
        long b = Math.abs((long)divisor);
        int result = 0;
        while (a >= b) {
            int shift = 0;
            while (a >= (b << shift)) {
                shift++;
            }
            a -= b << (shift - 1);
            result += 1 << (shift - 1);
        }
        return isNegative? -result: result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)