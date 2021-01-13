# 是子序列吗？
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/is-subsequence/?utm_source=sc-github-wzz)
 ## 题目描述
 给定字符串`s`和`t`，判断`s`是否为`t`的子序列。

你可以认为在`s`和`t`中都只包含小写字母。`t`可能是一个非常长（`length ~= 500,000`）的字符串，而`s`是一个较短的字符串（`length <= 100`）。

一个字符串的子序列是在原字符串中删去一些字符（也可以不删除）后，不改变剩余字符的相对位置形成的新字符串（例如，`"ace"`是`"abcde"`的子序列而`"aec"`不是）。
 ### 样例说明
 **样例1：**
```
输入：s = "abc"，t = "ahbgdc"
输出：true
```
**样例2：**
```
输入：s = "axc"，t = "ahbgdc"
输出：false
```
 ### 参考代码
 直接按s串的顺序去遍历t串即可。
```java
public class Solution {
    public boolean isSubsequence(String s, String t) {
        int i = 0, j = 0;
        while(i<s.length() && j < t.length()) {
            if(s.charAt(i) == t.charAt(j)) {
                i++;
            }
            j++;
        }
        return i == s.length();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)