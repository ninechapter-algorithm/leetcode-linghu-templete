# 大小写转换 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/lowercase-to-uppercase-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 将一个字符串中的小写字母转换为大写字母。不是字母的字符不需要做改变。
 ### 样例说明
 **样例 1:**

```
输入: str = "abc"
输出: "ABC"
```
**样例 2:**

```
输入: str = "aBc"
输出: "ABC"
```
**样例 3:**

```
输入: str = "abC12"
输出: "ABC12"
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param str a string
     * @return a string
     */
    public String lowercaseToUppercase2(String str) {
        // Write your code here
        StringBuilder sb = new StringBuilder(str);
        //遍历整个字符串，将所有的小写字母转成大写字母
        for (int index = 0; index < sb.length(); index++) {
            char c = sb.charAt(index);
            if (Character.isLowerCase(c)) {
                sb.setCharAt(index, Character.toUpperCase(c));
            }
        }
        return sb.toString();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)