# 反转整数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/reverse-integer/?utm_source=sc-github-wzz)
 ## 题目描述
 将一个整数中的数字进行颠倒，当颠倒后的整数溢出时，返回 0 (标记为 32 位整数)。
 ### 样例说明
 
**样例 1：**
```
输入：123
输出：321
```
**样例 2：**
```
输入：-123
输出：-321
```
 ### 参考代码
 Reverse digits of an integer.&nbsp;<div><br></div><div>Example1: x = 123, return 321&nbsp;</div><div>Example2: x = -123, return -321&nbsp;</div><div><br></div><div>Have you thought about this?
Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!&nbsp;</div><div>If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.&nbsp;</div><div>Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?&nbsp;</div><div>&nbsp;Throw an exception? Good, but what if throwing an exception is not an option? You would then have to re-design the function (ie, add an extra parameter).<div><br></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博:</span><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">&nbsp;&nbsp;</span><a href="http://weibo.com/3948019741/BAKMpkQmg" target="_blank">http://weibo.com/3948019741/BAKMpkQmg</a><br></div></div>
```java
public class Solution {
    /**
     * @param n the integer to be reversed
     * @return the reversed integer
     */
    public int reverseInteger(int n) {
        int reversed_n = 0;
        
        while (n != 0) {
            int temp = reversed_n * 10 + n % 10;
            n = n / 10;
            if (temp / 10 != reversed_n) {
                reversed_n = 0;
                break;
            }
            reversed_n = temp;
        }
        return reversed_n;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)