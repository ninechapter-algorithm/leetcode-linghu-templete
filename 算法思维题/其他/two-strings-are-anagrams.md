# 两个字符串是变位词
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/two-strings-are-anagrams/?utm_source=sc-github-wzz)
 ## 题目描述
 写出一个函数 `anagram(s, t)` 判断两个字符串是否可以通过改变字母的顺序变成一样的字符串。
 ### 样例说明
 
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param s: The first string
     * @param b: The second string
     * @return true or false
     */
    public boolean anagram(String s, String t) {
        // write your code here
        int[] cntS = new int[256];
        int[] cntT = new int[256];
        int i;
        for (i = 0; i < 256; ++i) {
            cntS[i] = cntT[i] = 0;
        }
        
        for (i = 0; i < s.length(); ++i) {
            cntS[(int)s.charAt(i)]++;
        }
        
        for (i = 0; i < t.length(); ++i) {
            cntT[(int)t.charAt(i)]++;
        }
        
        for (i = 0; i < 256; i++) {
            if (cntS[i] != cntT[i]) {
                return false;
            }
        }
        
        return true;
    }
}


// version: 高频题班
public class Solution {
    /**
     * @param s: The first string
     * @param b: The second string
     * @return true or false
     */
    public boolean anagram(String s, String t) {
        // write your code here
        int[] cntS = new int[256];
        int[] cntT = new int[256];
        for (char c : s.toCharArray()) {
            cntS[c]++;
        }
        for (char c : t.toCharArray()) {
            cntT[c]++;
        }
        for (int i = 0; i < 256; i++) {
            if (cntS[i] != cntT[i]) {
                return false;
            }
        }
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)