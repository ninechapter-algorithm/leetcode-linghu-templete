# 检查缩写字
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/valid-word-abbreviation/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个**非空字符串** `word` 和缩写 `abbr`，返回字符串是否可以和给定的缩写匹配。
比如一个 `“word”` 的字符串仅包含以下有效缩写：
```
["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
```
 ### 样例说明
 **样例 1:**
```
输入 : s = "internationalization", abbr = "i12iz4n"
输出 : true
```
**样例 2:**
```
输入 : s = "apple", abbr = "a2e"
输出 : false
```
 ### 参考代码
 用两个指针i,j分别从头开始匹配，j遇到数字，就先把数字x解析出来，然后i移动x位，继续匹配。如果不能匹配就返回false。
```java
public class Solution {
    public boolean validWordAbbreviation(String word, String abbr) {
        int i = 0, j = 0;
        while (i < word.length() && j < abbr.length()) {
            if (word.charAt(i) == abbr.charAt(j)) {
                i++;
                j++;
            } else if ((abbr.charAt(j) > '0') && (abbr.charAt(j) <= '9')) {     //notice that 0 cannot be included
                int start = j;
                while (j < abbr.length() && Character.isDigit(abbr.charAt(j))) {
                    j++;
                }
                i += Integer.valueOf(abbr.substring(start, j));
            } else {
                return false;
            }
        }
        return (i == word.length()) && (j == abbr.length());
    }
}


//version 高频班
public class Solution {
    /**
     * @param word: a non-empty string
     * @param abbr: an abbreviation
     * @return: true if string matches with the given abbr or false
     */
    public boolean validWordAbbreviation(String word, String abbr) {
        // write your code here
        int i = 0, j =0;
        char[] s = word.toCharArray();
        char[] t = abbr.toCharArray();
        
        while (i < s.length && j < t.length) {
            if (Character.isDigit(t[j])) {
                if (t[j] == '0') {
                    return false;
                }
                int val = 0;
                while (j < t.length && Character.isDigit(t[j])) {
                    val = val * 10 + t[j] - '0';
                    j++;
                }
                i += val;
            } else {
                if (s[i++] != t[j++]) {
                    return false;
                }
            }
        }
        return i == s.length && j == t.length;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)