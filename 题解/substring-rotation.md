# 用isSubstring判断字符串的循环移动
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/substring-rotation/?utm_source=sc-github-wzz)
 ## 题目描述
 假定有一种 isSubstring 的方法，可以检验某个单词是否为另一个单词的子字符串。给定 `s1` 和 `s2`，请设计一种方法来检验 s2 是否为 s1 的循环移动后的字符串。注意，只能调用一次 isSubstring 。
 ### 样例说明
 **样例 1：**
```
输入：s1 = "waterbottle", s2 = "erbottlewat"
输出：True
解释："waterbottle" 是 "erbottlewat" 的一种循环移动后的字符串。
```
**样例 2：**
```
输入：s1 = "apple", s2 = "ppale"
输出：False
解释："apple" 不是 "ppale" 的一种循环移动后的字符串。
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param s1 the first string
     * @param s2 the second string
     * @return true if s2 is a rotation of s1 or false
     */
    public boolean isRotation(String s1, String s2) {
        // Write your code here
        // Using one call to isSubstring
        int len = s1.length();
        /* check that s1 and s2 are equal length and not empty */
        if (len == s2.length() && len > 0) {
            /* concatenate s1 and s1 within new buffer */
            String s1s1 = s1 + s1;
            return isSubstring(s1s1, s2);
        }
        return false;
    }
    
    // @return true if t is a substring of s or false
    public boolean isSubstring(String s, String t) {
        return s.contains(t);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)