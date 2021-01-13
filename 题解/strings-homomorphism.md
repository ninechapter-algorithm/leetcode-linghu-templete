# 字符同构
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/strings-homomorphism/?utm_source=sc-github-wzz)
 ## 题目描述
 给定两个字符串 **s** 和 **t** ，确定它们是否是同构的。
两个字符串是同构的如果 s 中的字符可以被替换得到 t。
所有出现的字符必须用另一个字符代替，同时保留字符串的顺序。 没有两个字符可以映射到同一个字符，但一个字符可以映射到自己。
 ### 样例说明
 
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param s a string
     * @param t a string
     * @return true if the characters in s can be replaced to get t or false
     */
    public boolean isIsomorphic(String s, String t) {
        // Write your code here
        int[] m1 = new int[128];
        int[] m2 = new int[128];
        for (int i = 0; i < s.length(); ++i) {
            int cs = (int) s.charAt(i);
            int ts = (int) t.charAt(i);
            if (m1[cs] == 0 && m2[ts] == 0) {
                m1[cs] = ts;
                m2[ts] = 1;
            } else if (m1[cs] != ts) {
                return false;
            }
        }
        return true;
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param s a string
     * @param t a string
     * @return true if the characters in s can be replaced to get t or false
     */
    public boolean isIsomorphic(String s, String t) {
        // Write your code here
        int[] map = new int[256];  // ASCII 的范围是0-255
        char[] sc = s.toCharArray();
        char[] tc = t.toCharArray();

        for (int i = 0; i < s.length(); i++) {
            if (map[sc[i]] == 0) {
                map[sc[i]] = tc[i];
            } else {
                if (map[sc[i]] != tc[i]) {
                    return false;
                }
            }
        }

        int[] map2 = new int[256];
        for (int i = 0; i < t.length(); i++) {
            if (map2[tc[i]] == 0) {
                map2[tc[i]] = sc[i];
            } else {
                if (map2[tc[i]] != sc[i]) {
                    return false;
                }
            }
        }

        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)