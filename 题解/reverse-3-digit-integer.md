# 反转一个3位整数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/reverse-3-digit-integer/?utm_source=sc-github-wzz)
 ## 题目描述
 反转一个只有3位数的整数。
 ### 样例说明
 **样例 1:**

```
输入: number = 123
输出: 321
```
**样例 2:**

```
输入: number = 900
输出: 9
```

 ### 参考代码
 硅谷求职算法集训营上课版本
```java
public class Solution {
    /*
     * @param number: A 3-digit number.
     * @return: Reversed number.
     */
    public int reverseInteger(int number) {
        // write your code here
        //获得个位数
        int num1 = number % 10;
        //获得十位数
        int num2 = (number / 10) % 10;
        //获得百位数
        int num3 = ((number / 10) / 10) % 10;
        //相加
        return num3 + num2 * 10 + num1 * 100;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)