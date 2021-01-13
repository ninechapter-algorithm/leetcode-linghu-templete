# 字符大小写排序
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sort-letters-by-case/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="line-height: 1.42857143;">给定一个只包含字母的字符串，按照先小写字母后大写字母的顺序进行排序。</span></p>
 ### 样例说明
 ```
样例 1:
	输入:  "abAcD"
	输出:  "acbAD"

样例 2:
	输入: "ABC"
	输出:  "ABC"
	
```
 ### 参考代码
 ```java
public class Solution {
    public void sortLetters(char[] chars) {
        int i = 0, j = chars.length - 1;
        
        while (i <= j) {
            while (i <= j && Character.isLowerCase(chars[i])) {
                i++;
            }
            while (i <= j && Character.isUpperCase(chars[j])) {
                j--;
            }
            if (i <= j) {
                char tmp = chars[i];
                chars[i] = chars[j];
                chars[j] = tmp;
                i++;
                j--;
            }
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)