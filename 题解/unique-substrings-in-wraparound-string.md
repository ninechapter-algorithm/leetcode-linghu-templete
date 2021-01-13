# 环绕字符串中的唯一子串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/unique-substrings-in-wraparound-string/?utm_source=sc-github-wzz)
 ## 题目描述
 字符串`s`是由字符串`"abcdefghijklmnopqrstuvwxyz"`无限重复环绕形成的，所以`s`看起来像是这样：`"...zabcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyzabcd...."`。

现在有另一个字符串`p`。你的任务是找出`p`中有多少互不相同的非空子串出现在`s`中。确切的说，你得到字符串`p`作为输入，你需要输出关于`p`非空子串的数目，这些子串互不相同，并且能在`s`中被找到。
 ### 样例说明
 样例1：
```
输入："a"
输出：1
说明：字符串"a"的所有非空子串中，只有"a"出现在字符串s中。
```

样例2：
```
输入："cac"
输出：2
说明：字符串"cac"的所有非空子串中，"a"和"c"出现在字符串s中。
```

样例3：
```
输入："zab"
输出：6
说明：有六个"zab"的非空子串"z"、"a"、"b"、"za"、"ab"、"zab"出现在字符串s中。
```
 ### 参考代码
 用动态规划来维护以每一个字母为末尾的最长子串长度，长度相加即为答案
```java
public class Solution {
    public int findSubstringInWraproundString(String p) {
        int []dp=new int[26];
        for(int i = 0;i < 26;i++)
        dp[i]=0;
        int len=p.length();
        int pos = 0;
        for(int i = 0;i < len;i++){
            if(i > 0 && (p.charAt(i) - p.charAt(i-1) == 1 || p.charAt(i) == 'a' && p.charAt(i-1) == 'z')){
                pos ++;
            }
            else{
                pos = 1;
            }
            dp[p.charAt(i) - 'a'] = Math.max(dp[p.charAt(i) - 'a'],pos);
        }
        int ans = 0;
        for(int i = 0;i < 26;i++){
            ans+=dp[i];
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)