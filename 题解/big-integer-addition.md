# big integer addition
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/big-integer-addition/?utm_source=sc-github-wzz)
 ## 题目描述
 1784
 ### 样例说明
 1784
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param num1 a non-negative integers
     * @param num2 a non-negative integers
     * @return return sum of num1 and num2
     */
    public String addStrings(String num1, String num2) {
        // Write your code here
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        int carry = 0;
        String result = "";
        while (i >= 0 || j >= 0) {
            if (i >= 0) {
                carry += num1.charAt(i--) - '0';
            }
            if (j >= 0) {
                carry += num2.charAt(j--) - '0';
            }
            result = carry % 10 + result;
            carry /= 10;
        }
        return carry > 0 ? "1" + result : result;
    }
}


// version: 高频题班
public class Solution {
    /**
     * @param num1 a non-negative integers
     * @param num2 a non-negative integers
     * @return return sum of num1 and num2
     */
    public String addStrings(String num1, String num2) {
        // Write your code here
        String ans = "";

        int carry = 0;
        for (int i = num1.length() - 1, j = num2.length() - 1; i >= 0 || j >= 0; i--, j--) {
            int sum = carry;
            sum += (i >= 0) ? num1.charAt(i) - '0' : 0;
            sum += (j >= 0) ? num2.charAt(j) - '0' : 0;
            ans = (sum % 10) + ans;
            carry = sum / 10;
        }
        if (carry != 0) {
            ans = carry + ans;
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)