# 大整数乘法
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/multiply-strings/?utm_source=sc-github-wzz)
 ## 题目描述
 以字符串的形式给定两个非负整数 `num1` 和 `num2`，返回 `num1` 和 `num2` 的乘积。
 ### 样例说明
 **样例1**
```
输入：
"123"
"45"
输出：
"5535"
解释：
123 x 45 = 5535
```
**样例2**
```
输入：
"0"
"0"
输出：
"0"
```
 ### 参考代码
 Given two numbers represented as strings, return multiplication of the numbers as a string.

Note: The numbers can be arbitrarily large and are non-negative.

模拟竖式的计算过程来计算结果。
```java
public class Solution {
    public String multiply(String num1, String num2) {
        if (num1 == null || num2 == null) {
            return null;
        }
        
        int len1 = num1.length(), len2 = num2.length();
        int len3 = len1 + len2;
        int i, j, product, carry;

        int[] num3 = new int[len3];
        for (i = len1 - 1; i >= 0; i--) {
            carry = 0;
            for (j = len2 - 1; j >= 0; j--) {
                product = carry + num3[i + j + 1] +
                    Character.getNumericValue(num1.charAt(i)) *
                    Character.getNumericValue(num2.charAt(j));
                num3[i + j + 1] = product % 10;
                carry = product / 10;
            }
            num3[i + j + 1] = carry;
        }

        StringBuilder sb = new StringBuilder();
        i = 0;

        while (i < len3 - 1 && num3[i] == 0) {
            i++;
        }

        while (i < len3) {
            sb.append(num3[i++]);
        }

        return sb.toString();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)