# 最后一个单词的长度
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/length-of-last-word/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串， 包含大小写字母、空格 `' '`，请返回其最后一个单词的长度。

如果不存在最后一个单词，请返回 `0` 。
 ### 样例说明
 
**样例 1：**
```
输入："Hello World"
输出：5
```
**样例 2：**
```
输入："Hello LintCode"
输出：8
```
 ### 参考代码
 Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

For example, 
Given s = "Hello World",
return 5.
```java
public class Solution {
    public int lengthOfLastWord(String s) {
        int length = 0;
        char[] chars = s.toCharArray();
        for (int i = s.length() - 1; i >= 0; i--) {
            if (length == 0) {
                if (chars[i] == ' ') {
                    continue;
                } else {
                    length++;
                }
            } else {
                if (chars[i] == ' ') {
                    break;
                } else {
                    length++;
                }
            }
        }

        return length;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)