# big integer multiplication
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/big-integer-multiplication/?utm_source=sc-github-wzz)
 ## 题目描述
 1783
 ### 样例说明
 1783
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param num1 a non-negative integers
     * @param num2 a non-negative integers
     * @return return product of num1 and num2
     */
    public String multiply(String num1, String num2) {
        // Write your code here
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



// version: 高频题班
public class Solution {
    /**
     * @param num1 a non-negative integers
     * @param num2 a non-negative integers
     * @return return product of num1 and num2
     */
    public String multiply(String num1, String num2) {
        // Write your code here
        int l1 = num1.length();
        int l2 = num2.length();

        int[] ans = new int[l1 + l2 + 1];
        for (int i = 0; i < l1; i++) {
            for (int j = 0; j < l2; j++) {
                ans[i + j] += (num1.charAt(l1 - 1 - i) - '0') * (num2.charAt(l2 - 1 - j) - '0');
            }
        }

        for (int i = 0; i < l1 + l2; i++) {
            ans[i + 1] += ans[i] / 10;
            ans[i] %= 10;
        }

        int i = l1 + l2;
        while (ans[i] == 0 && i >= 1) {
            i--;
        }
        String str = "";
        while (i >= 0) {
            str += ans[i--];
        }
        return str;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)