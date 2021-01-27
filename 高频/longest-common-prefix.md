# 最长公共前缀
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-common-prefix/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给k个字符串，求出他们的最长公共前缀(LCP)</p>
 ### 样例说明
 ```
样例 1:
	输入:  "ABCD", "ABEF", "ACEF"
	输出:  "A"
	

样例 2:
	输入: "ABCDEFG", "ABCEFG" and "ABCEFA"
	输出:  "ABC"

```
 ### 参考代码
 Write a function to find the longest common prefix string amongst an array of strings.


直接模拟比较即可。
```java
public class Solution {
    
    // 1. Method 1, start from the first one, compare prefix with next string, until end;
    // 2. Method 2, start from the first char, compare it with all string, and then the second char
    // I am using method 1 here
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        String prefix = strs[0];
        for(int i = 1; i < strs.length; i++) {
            int j = 0;
            while( j < strs[i].length() && j < prefix.length() && strs[i].charAt(j) == prefix.charAt(j)) {
                j++;
            }
            if( j == 0) {
                return "";
	    }
            prefix = prefix.substring(0, j);
        }
        return prefix;
    }

}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)