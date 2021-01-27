# 最短回文串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/shortest-palindrome/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个字符串 `S`, 你可以通过在前面添加字符将其转换为回文串.找到并返回用这种方式转换的最短回文串.
 ### 样例说明
 **样例1**
```
输入： "aacecaaa"
输出： "aaacecaaa"
解释：
在输入字符串前面添加一个'a'。
```
**样例2**
```
输入： "abcd"
输出： "dcbabcd"
````
 ### 参考代码
 从后往前每次减去一个字符后子串是否为回文串。
答案为将减去的部分翻转后接入最前面。
```java
public class Solution {

    public String shortestPalindrome(String s) {

        int j = 0;

        for (int i = s.length() - 1; i >= 0; i--) {//找到第一个使他不回文的位置

           if (s.charAt(i) == s.charAt(j)) { 

               j += 1; 

           }

        }

        if (j == s.length()) {  //本身是回文

            return s; 

        }

        String suffix = s.substring(j); // 后缀不能够匹配的字符串

        String prefix = new StringBuilder(suffix).reverse().toString(); // 前面补充prefix让他和suffix回文匹配

        String mid = shortestPalindrome(s.substring(0, j)); //递归调用找 [0,j]要最少可以补充多少个字符让他回文

        String ans = prefix + mid  + suffix;

        return  ans;

    }

}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)