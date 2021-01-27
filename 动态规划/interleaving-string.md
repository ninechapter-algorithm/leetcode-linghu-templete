# 交叉字符串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/interleaving-string/?utm_source=sc-github-wzz)
 ## 题目描述
 给出三个字符串:*s1*、*s2*、*s3*，判断*s3*是否由*s1*和*s2*交叉构成。
 ### 样例说明
 
**样例 1：**
```
输入:
"aabcc"
"dbbca"
"aadbbcbcac"
输出:
true
```
**样例 2：**
```
输入:
""
""
"1"
输出:
false
```
**样例 3：**
```
输入:
"aabcc"
"dbbca"
"aadbbbaccc"
输出:
false
```

 ### 参考代码
 动态规划。
dp[i][j]代表由s1的前i个字母和s2的前j个字母是否能构成当前i+j个字母。
然后状态转移即可。（看第i+j+1个是否能被s1的第i+1个构成或被s2的第j+1个构成）
```java
public class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1.length() + s2.length() != s3.length()) {
            return false;
        }
        
        boolean [][] interleaved = new boolean[s1.length() + 1][s2.length() + 1];
        interleaved[0][0] = true;
        
        for (int i = 1; i <= s1.length(); i++) {
            if(s3.charAt(i - 1) == s1.charAt(i - 1) && interleaved[i - 1][0])
                interleaved[i][0] = true;
        }
        
        for (int j = 1; j <= s2.length(); j++) {
            if(s3.charAt(j - 1) == s2.charAt(j - 1) && interleaved[0][j - 1])
                interleaved[0][j] = true;
        }
        
        for (int i = 1; i <= s1.length(); i++) {
            for (int j = 1; j <= s2.length(); j++) {
                if(((s3.charAt(i + j - 1) == s1.charAt(i - 1) && interleaved[i - 1][j]))
                    || ((s3.charAt(i + j - 1)) == s2.charAt(j - 1) && interleaved[i][j - 1]))
                interleaved[i][j] = true;
            }
        }
        
        return interleaved[s1.length()][s2.length()];
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)