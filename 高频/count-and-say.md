# 报数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/count-and-say/?utm_source=sc-github-wzz)
 ## 题目描述
 报数指的是，按照其中的整数的顺序进行报数，然后得到下一个数。如下所示：

`1, 11, 21, 1211, 111221, ...`

`1` 读作 `"one 1"` -> `11`

`11` 读作 `"two 1s"` -> `21`

`21` 读作 `"one 2, then one 1"` -> `1211`

给定一个整数 `n`, 返回 第 `n` 个顺序。 
 ### 样例说明
 
**样例 1：**
```
输入：1
输出："1"
```
**样例 2：**
```
输入：5
输出："111221"
```
 ### 参考代码
 The count-and-say sequence is the sequence of integers beginning as follows:
1, 11, 21, 1211, 111221, ...

1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.
Given an integer n, generate the nth sequence.

Note: The sequence of integers will be represented as a string.
```java
public class Solution {
    public String countAndSay(int n) {
        String oldString = "1";
        while (--n > 0) {
            StringBuilder sb = new StringBuilder();
            char [] oldChars = oldString.toCharArray();

            for (int i = 0; i < oldChars.length; i++) {
                int count = 1;
                while ((i+1) < oldChars.length && oldChars[i] == oldChars[i+1]) {
                    count++;
                    i++;
                }
                sb.append(String.valueOf(count) + String.valueOf(oldChars[i]));
            }
            oldString = sb.toString();
        }

        return oldString;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)