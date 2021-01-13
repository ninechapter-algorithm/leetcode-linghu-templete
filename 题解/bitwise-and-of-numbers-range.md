#  数字范围内位的与
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/bitwise-and-of-numbers-range/?utm_source=sc-github-wzz)
 ## 题目描述
 给定范围[m，n]，其中0 <= m <= n <= 2147483647，输出此范围内所有数字的按位AND，包括端值。

例如，给定范围[5,7]，输出返回4。
 ### 样例说明
 **样例1**

```
输入: m=5, n=7
输出: 4
```

**样例2**

```
输入: m=14, n=15
输出: 14
```
 ### 参考代码
 本题中，我们需要得到[m,n]所有元素按位与的结果。举个例子，当m=26，n=30时，它们的二进制表示为为：
**11**010　　**11**011　　**11**100　　**11**101　　**11**110
这个样例的答案是**11**000，易见我们发现我们只需要找到m和n最左边的公共部分即可。

每次都将n与n-1按位与，当n的二进制为1010时，1010 & 1001 = 1000，相当于把二进制位的最后一个1去掉了。因此我们不断的做n^n-1的操作，直到n小于m相等即可。
```java
public class Solution {
    /**
     * @param m: an Integer
     * @param n: an Integer
     * @return: the bitwise AND of all numbers in [m,n]
     */
    public int rangeBitwiseAnd(int m, int n) {
        // Write your code here
        while(m < n) {
            n = n & (n-1);
        }
        return n;
        
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)