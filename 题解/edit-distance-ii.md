# 一次编辑距离
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/edit-distance-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定两个字符串 S 和 T, 判断T是否可以通过对S做刚好一次编辑得到。
每次编辑可以选择以下任意一个操作：
- 在S的任意位置插入一个字符
- 删除S中的任意一个字符
- 将S中的任意字符替换成其他字符
 ### 样例说明
 
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param s a string
     * @param t a string
     * @return true if they are both one edit distance apart or false
     */
    public boolean isOneEditDistance(String s, String t) {
        // Write your code here
        int m = s.length();
        int n = t.length();
        if (Math.abs(m - n) > 1)
            return false;

        if (m > n)
            return isOneEditDistance(t, s);
        for (int i = 0; i < m; i++) {
            if (s.charAt(i) != t.charAt(i)) {
                if (m == n) {
                    return s.substring(i + 1).equals(t.substring(i + 1));
                }
                return s.substring(i).equals(t.substring(i + 1));
            }
        }
        return m != n;
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param s a string
     * @param t a string
     * @return true if they are both one edit distance apart or false
     */
    public boolean isOneEditDistance(String s, String t) {
        // Write your code here
        if (s.length() > t.length()) {
            return isOneEditDistance(t, s);
        }
        int diff = t.length() - s.length();

        if (diff > 1) {
            return false;
        }
        if (diff == 0) {
            int cnt = 0;
            for (int i = 0; i < s.length(); i++) {
                if (t.charAt(i) != s.charAt(i)) {
                    cnt++;
                }
            }
            return (cnt == 1);
        }
        if (diff == 1) {
            for (int i = 0; i < s.length(); i++) {
                if (t.charAt(i) != s.charAt(i)) {
                    return (s.substring(i).equals(t.substring(i + 1)));
                }
            }
        }
        return true;
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)