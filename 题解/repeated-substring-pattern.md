# 重复的子串模式
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/repeated-substring-pattern/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个非空字符串，判断它能否通过重复它的某一个子串若干次（两次及以上）得到。字符串由小写字母组成，并且它的长度不会超过10000。


 ### 样例说明
 **样例1：**
~~~~.
输入："abab"

输出：True

说明：可以由它的子串"ab"重复两次得到。
~~~~
**样例2：**
~~~~.
输入："aba"

输出：False
~~~~
**样例3：**
~~~~.
输入："abcabcabcabc"

输出：True

说明：可以由它的子串"abc"重复四次得到（同时也可以是"abcabc"重复两次）。
~~~~
 ### 参考代码
 KMP算法对于next数组的应用。
next\[i\]是指对于字符串s\[0,i-1\]中，前缀与后缀的最大匹配长度。
例如对于"abcabcabc"来说，其next\[8\] = 5，也即对于s\[0,7\]="abcabcab"，前缀与后缀最大匹配的串为"abcab"，长度为5。
用字符串长度减1减去最后一位的next数组值之后得到的应为重复串的长度。
```java
public class Solution {
    public boolean repeatedSubstringPattern(String s) {
        int l = s.length();
        int[] next = new int[l];
        next[0] = -1;
        int i, j = -1;
        for (i = 1; i < l; i++) {
            while (j >= 0 && s.charAt(i) != s.charAt(j + 1)) {
                j = next[j];
            }
            if (s.charAt(i) == s.charAt(j + 1)) {
                j++;
            }
            next[i] = j;
        }
        int lenSub = l - 1 - next[l - 1];
        return lenSub != l && l % lenSub ==0;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)