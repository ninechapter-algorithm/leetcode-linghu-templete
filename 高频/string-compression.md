# 字符串压缩
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/string-compression/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一种方法，通过给重复字符计数来进行基本的字符串压缩。

例如，字符串 `aabcccccaaa` 可压缩为 `a2b1c5a3` 。而如果压缩后的字符数不小于原始的字符数，则返回原始的字符串。

可以假设字符串仅包括 a-z 的字母。
 ### 样例说明
 **样例 1：**
```
输入：str = "aabcccccaaa"
输出："a2b1c5a3"
```
**样例 2：**
```
输入：str = "aabbcc"
输出："aabbcc"
```
 ### 参考代码
 ```java
public class Solution {
    /**
     * @param str a string
     * @return a compressed string
     */
    public String compress(String str) {
        // Write your code here
        /* Check if compression would create a longer string */
        int size = countCompression(str);
        if (size >= str.length()) {
            return str;
        }

        char[] array = new char[size];
        int index = 0;
        char last = str.charAt(0);
        int count = 1;
        for (int i = 1; i < str.length(); i++) {
            if (str.charAt(i) == last) { // Found repeated character
                count++;
            } else {
                /* Update the repeated character count */
                index = setChar(array, last, index, count);
                last = str.charAt(i);
                count = 1;
            }
        }
        /* Update string with the last set of repeated characters. */
        index = setChar(array, last, index, count);
        return String.valueOf(array);
    }

    public int setChar(char[] array, char c, int index, int count) {
        array[index] = c;
        index++;
        char[] cnt = String.valueOf(count).toCharArray();

        /* Copy characters from biggest digit to smallest */
        for (char x : cnt) {
            array[index] = x;
            index++;
        }
        return index;
    }

    int countCompression(String str) {
        if (str == null || str.isEmpty()) return 0;
        char last = str.charAt(0);
        int size = 0;
        int count = 1;
        for (int i = 1; i < str.length(); i++) {
            if (str.charAt(i) == last) {
                count++;
            } else {
                last = str.charAt(i);
                size += 1 + String.valueOf(count).length();
                count = 1;
            }
        }
        size += 1 + String.valueOf(count).length();
        return size;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)