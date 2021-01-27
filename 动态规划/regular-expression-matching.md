# 正则表达式匹配
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/regular-expression-matching/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>实现支持<b><font color="#e76363">'.'</font></b>和<b><font color="#e76363">'*'</font></b>的<span style="line-height: 1.42857143;">正则表达式</span><span style="line-height: 1.42857143;">匹配。</span></p><p>'.'匹配任意一个字母。</p><p>'*'匹配零个或者多个前面的元素。</p><p>匹配应该覆盖整个输入字符串，而不仅仅是一部分。</p><p>需要实现的函数是：bool isMatch(string s, string p)</p>
<p>isMatch("aa","a") → false</p><p>isMatch("aa","aa") → true</p><p>isMatch("aaa","aa") → false</p><p>isMatch("aa", "a*") → true</p><p>isMatch("aa", ".*") → true</p><p>isMatch("ab", ".*") → true</p><p>isMatch("aab", "c*a*b") →  true</p>
 ### 样例说明
 **样例 1:**
```
输入："aa"，"a"
输出：false
解释：
无法匹配
```

**样例 2:**
```
输入："aa"，"a*"
输出：true
解释：
'*' 可以重复 a
```

 ### 参考代码
 和 Wildcard Matching 同样模板的代码。
使用了记忆化搜索（Memoization Search）

考点：
* 记忆化搜索|| dp

题解：
* 采用数组memo记录各处字符匹配情况，dfs递归进行搜索，记忆化剪枝
* 当前p串中有* ，就有两种选择，然后* 可以不去匹配，直接用p串的下一个匹配当前s串字符，或者重复p串的上一个字符匹配。
* .可以匹配任意字符
```java
public class Solution {
    /**
     * @param s: A string 
     * @param p: A string includes "." and "*"
     * @return: A boolean
     */
    public boolean isMatch(String s, String p) {
        if (s == null || p == null) {
            return false;
        }
        
        boolean[][] memo = new boolean[s.length()][p.length()];			//记忆搜索结果
        boolean[][] visited = new boolean[s.length()][p.length()];		//标记是否访问
        
        return isMatchHelper(s, 0, p, 0, memo, visited);
    }
    
    private boolean isMatchHelper(String s, int sIndex,
                                  String p, int pIndex,
                                  boolean[][] memo,
                                  boolean[][] visited) {
        // "" == ""
        if (pIndex == p.length()) {       //如果p已经匹配完毕
            return sIndex == s.length();	//根据s是否匹配完毕即可
        }
        
        if (sIndex == s.length()) {		//如果s匹配完毕
            return isEmpty(p, pIndex);
        }
        
        if (visited[sIndex][pIndex]) {
            return memo[sIndex][pIndex];
        }
        
        char sChar = s.charAt(sIndex);
        char pChar = p.charAt(pIndex);
        boolean match;
        
        // consider a* as a bundle
        if (pIndex + 1 < p.length() && p.charAt(pIndex + 1) == '*') {    	 //如果为'*'，有两种方案
            match = isMatchHelper(s, sIndex, p, pIndex + 2, memo, visited) ||                //'*'不去匹配字符
                charMatch(sChar, pChar) && isMatchHelper(s, sIndex + 1, p, pIndex, memo, visited);  //'*'重复前面一个字符去匹配s
        } else {
            match = charMatch(sChar, pChar) && 		//如果当前两字符匹配
                isMatchHelper(s, sIndex + 1, p, pIndex + 1, memo, visited); //继续下一个字符匹配
        }
        
        visited[sIndex][pIndex] = true;    //搜索完成就标记
        memo[sIndex][pIndex] = match;     //存储搜索结果
        return match;
    }
    
    private boolean charMatch(char sChar, char pChar) {		//判断两字符是否匹配
        return sChar == pChar || pChar == '.';
    }
    
    private boolean isEmpty(String p, int pIndex) {    //形如"x*x*"形式
        for (int i = pIndex; i < p.length(); i += 2) {
            if (i + 1 >= p.length() || p.charAt(i + 1) != '*') {   //如果不是'*'，无法匹配
                return false;
            }
        }
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)