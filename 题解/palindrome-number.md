# 回文数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/palindrome-number/?utm_source=sc-github-wzz)
 ## 题目描述
 判断一个正整数是不是回文数。

回文数的定义是，将这个数反转之后，得到的数仍然是同一个数。
 ### 样例说明
 例1：
```
输入：11
输出：true

```
例2：
```
输入：1232
输出：false
解释：
1232!=2321
```
 ### 参考代码
 Determine whether an integer is a palindrome. Do this without extra space.&nbsp;<div><br></div><div>Some hints:&nbsp;</div><div>Could negative integers be palindromes? (ie, -1)&nbsp;</div><div>&nbsp;If you are thinking of converting the integer to string, note the restriction of using extra space.&nbsp;</div><div>You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?&nbsp;</div><div>&nbsp;There is a more generic way of solving this problem.</div>
翻转整数，判断是否相等
```java
public class Solution {
    /**
     * @param num a positive number
     * @return true if it's a palindrome or false
     */
    public boolean isPalindrome(int x) {
        if(x < 0) {
            return false;
        }
        return x == reverse(x);    
    }
    
    public int reverse(int x) {
        int rst = 0;
        while(x != 0) {
            rst = rst * 10 + x % 10;
            x = x / 10;
        }
        return rst;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)