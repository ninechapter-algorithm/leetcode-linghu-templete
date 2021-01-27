# 大整数加法
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/add-strings/?utm_source=sc-github-wzz)
 ## 题目描述
 以字符串的形式给出两个非负整数 `num1` 和 `num2`，返回 `num1` 和 `num2` 的和。 
 ### 样例说明
 **样例 1:**
```
输入 : num1 = "123", num2 = "45"
输出 : "168"
```
 ### 参考代码
 将两个数解析后相加即可
```java
public class Solution {
    public String addStrings(String num1, String num2) {
        String res = "";
        int m = num1.length(), n = num2.length(), i = m - 1, j = n - 1, flag = 0;
        while(i >= 0 || j >= 0){
            int a, b; 
            if(i >= 0){
                a = num1.charAt(i--) - '0';
            }
            else{
                a = 0;
            }
            if(j >= 0){
                b = num2.charAt(j--) - '0';
            }
            else{
                b = 0;
            }
            int sum = a + b + flag;
            res =(char)(sum % 10 + '0') + res;
            flag = sum / 10;
        }
        return flag == 1 ? "1" + res: res; 
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)