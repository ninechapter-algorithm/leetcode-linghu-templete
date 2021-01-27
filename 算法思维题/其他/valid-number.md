# 有效数字
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/valid-number/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串，验证其是否为数字。
 ### 样例说明
 **样例 1:**

```
输入: "0"
输出: true
解释: "0" 可以被转换成 0
```

**样例 2:**

```
输入: "0.1"
输出: true
解释: "0.1" 可以被转换成 0.1
```

**样例 3:**

```
输入: "abc"
输出: false
```

**样例 4:**

```
输入: "1 a"
输出: false
```

**样例 5:**

```
输入: "2e10"
输出: true
解释: "2e10" 代表 20,000,000,000
```
 ### 参考代码
 首先应该明确合法的数字有哪些:

1. 整数, 例如 "122", "114"
2. 浮点数, 例如 "1.2", "2.", ".5", "1e10", "1E10"
3. 上面两种数加上符号, 即 "+" 或 "-"

"2.", ".5" 这两种形式可能让你有点迷惑, 你可以试一试, 在大多数编程语言中它们都是合法的字面量.

为了方便, 我们可以先处理掉首尾的空白字符. 然后再判断第一个是否符号, 如果是也过滤掉. 

然后, 剩下的字符串就只能包含 0-9, `.`, `e/E` 这三类字符了, 如果含有这三类之外的, 直接返回 false 即可. 然后根据以下原则判断即可:

1. 小数点和 `e/E` 都至多只能出现 1 次
2. 如果含有小数点, 则小数点前后至少有一个数字, 一个孤立的小数点是非法的.
3. 如果含有 `e/E`, 则它的前后必须有数字.
```java
// Non-regex version

public class Solution {
    public boolean isNumber(String s) {
        int len = s.length();
        int i = 0, e = len - 1;
        while (i <= e && Character.isWhitespace(s.charAt(i)))
            i++;
        if (i > len - 1)
            return false;
        while (e >= i && Character.isWhitespace(s.charAt(e)))
            e--;
        // skip leading +/-
        if (s.charAt(i) == '+' || s.charAt(i) == '-')
            i++;
        boolean num = false; // is a digit
        boolean dot = false; // is a '.'
        boolean exp = false; // is a 'e'
        while (i <= e) {
            char c = s.charAt(i);
            if (Character.isDigit(c)) {
                num = true;
            } else if (c == '.') {
                if (exp || dot)
                    return false;
                dot = true;
            } else if (c == 'e') {
                if (exp || num == false)
                    return false;
                exp = true;
                num = false;
            } else if (c == '+' || c == '-') {
                if (s.charAt(i - 1) != 'e')
                    return false;
            } else {
                return false;
            }
            i++;
        }
        return num;
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param s: the string that represents a number
     * @return: whether the string is a valid number
     */
    public boolean isNumber(String s) {
        // write your code here
        int i = 0;
        s = s.trim() + " "; // why +" "?
        char[] sc = s.toCharArray();
        int len = s.length() - 1;

        if (sc[i] == '+' || sc[i] == '-') {
            i++;
        }
        int nDigit = 0, nPoint = 0;
        while (Character.isDigit(sc[i]) || sc[i] == '.') {
            if (Character.isDigit(sc[i])) {
                nDigit++;
            }
            if (sc[i] == '.') {
                nPoint++;
            }
            i++;
        }
        if (nDigit <= 0 || nPoint > 1) {
            return false;
        }

        if (sc[i] == 'e') {
            i++;
            if (sc[i] == '+' || sc[i] == '-') {
                i++;
            }
            if (i == len) {
                return false;
            }
            for (; i < len; i++) {
                if (!Character.isDigit(sc[i])) {
                    return false;
                }
            }
        }
        return i == len;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)