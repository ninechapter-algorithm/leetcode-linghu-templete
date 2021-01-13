# 尾部的零
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/trailing-zeros/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>设计一个算法，计算出n阶乘中尾部零的个数</p>
 ### 样例说明
 ```
样例  1:
	输入: 11
	输出: 2
	
	样例解释: 
	11! = 39916800, 结尾的0有2个。

样例 2:
	输入:  5
	输出: 1
	
	样例解释: 
	5! = 120， 结尾的0有1个。

```
 ### 参考代码
 可以将每个数拆分成其素因子的乘积，可以发现，0是由`2*5`产生的，而5的数量一定小于2的数量，因此5的个数决定了结尾0的个数。

只要计算n的阶乘中，5这个素因子出现多少次即可。
```java
class Solution {
    /*
     * param n: As desciption
     * return: An integer, denote the number of trailing zeros in n!
     */
    public long trailingZeros(long n) {
        long sum = 0;
        while (n != 0) {
            sum += n / 5;
            n /= 5;
        }
        return sum;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)