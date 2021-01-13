# 大小写转换
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/lowercase-to-uppercase/?utm_source=sc-github-wzz)
 ## 题目描述
 将一个字符由小写字母转换为大写字母
 ### 样例说明
 **样例 1:**

```
输入: 'a'
输出: 'A'
```
**样例 2:**

```
输入: 'b'
输出: 'B'
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param character a character
     * @return a character
     */
    public char lowercaseToUppercase(char character) {
        // Write your code here
        //获得character与'a'的差值，在'A'的基础上加上这个差值
        return (char)(character - 'a' + 'A');
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)