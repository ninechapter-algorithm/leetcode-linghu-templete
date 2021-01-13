# 通配符匹配
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/wildcard-matching/?utm_source=sc-github-wzz)
 ## 题目描述
 判断两个可能包含通配符“？”和“*”的字符串是否匹配。匹配规则如下：

- '?' 可以匹配任何单个字符。
- '*' 可以匹配任意字符串（包括空字符串）。

两个串完全匹配才算匹配成功。

 ### 样例说明
 **样例1**

```plain
输入:
"aa"
"a"
输出: false
```

**输出2**

```plain
输入:
"aa"
"aa"
输出: true
```

**输出3**

```plain
输入:
"aaa"
"aa"
输出: false
```

**输出4**

```plain
输入:
"aa"
"*"
输出: true
说明: '*' 可以替换任何字符串
```

**输出5**

```plain
输入:
"aa"
"a*"
输出: true
```

**样例6**

```plain
输入:
"ab"
"?*"
输出: true
说明: '?' -> 'a' '*' -> 'b'
```

**样例7**

```plain
输入:
"aab"
"c*a*b"
输出: false
```


 ### 参考代码
 使用深度优先搜索 + 记忆化的版本。

用一个二维的 boolean 数组来当记忆化数组，记录 s 从 sIndex 开始的后缀 能够匹配上 p 从 pIndex 开始的后缀
```java
public class Solution {
    /**
     * @param s: A string 
     * @param p: A string includes "?" and "*"
     * @return: is Match?
     */
    public boolean isMatch(String s, String p) {
        if (s == null || p == null) {
            return false;
        }
        
        boolean[][] memo = new boolean[s.length()][p.length()];
        boolean[][] visited = new boolean[s.length()][p.length()];
        return isMatchHelper(s, 0, p, 0, memo, visited);
    }
    
    private boolean isMatchHelper(String s, int sIndex,
                                  String p, int pIndex,
                                  boolean[][] memo,
                                  boolean[][] visited) {
        // 如果 p 从pIdex开始是空字符串了，那么 s 也必须从 sIndex 是空才能匹配上
        if (pIndex == p.length()) {
            return sIndex == s.length();
        }
        
        // 如果 s 从 sIndex 是空，那么p 必须全是 * 
        if (sIndex == s.length()) {
            return allStar(p, pIndex);
        }
        
        if (visited[sIndex][pIndex]) {
            return memo[sIndex][pIndex];
        }
        
        char sChar = s.charAt(sIndex);
        char pChar = p.charAt(pIndex);
        boolean match;
        
        if (pChar == '*') {
            match = isMatchHelper(s, sIndex, p, pIndex + 1, memo, visited) ||
                isMatchHelper(s, sIndex + 1, p, pIndex, memo, visited);
        } else {
            match = charMatch(sChar, pChar) &&
                isMatchHelper(s, sIndex + 1, p, pIndex + 1, memo, visited);
        }
        
        visited[sIndex][pIndex] = true;
        memo[sIndex][pIndex] = match;
        return match;
    }
    
    private boolean charMatch(char sChar, char pChar) {
        return (sChar == pChar || pChar == '?');
    }
    
    private boolean allStar(String p, int pIndex) {
        for (int i = pIndex; i < p.length(); i++) {
            if (p.charAt(i) != '*') {
                return false;
            }
        }
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)