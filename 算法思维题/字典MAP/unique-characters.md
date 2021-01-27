# 判断字符串是否没有重复字符
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/unique-characters/?utm_source=sc-github-wzz)
 ## 题目描述
 实现一个算法确定字符串中的字符是否均唯一出现
 ### 样例说明
 **样例 1:**

```
输入:  "abc_____"
输出:  false
```

**样例 2:**

```
输入:  "abc"
输出:  true	
```
 ### 参考代码
 使用一个map或数组标记每个字符是否出现过。
```java
public class Solution {
    /**
     * @param str: a string
     * @return: a boolean
     */
    public boolean isUnique(String str) {
        // write your code here
        boolean[] char_set = new boolean[256];
        for (int i = 0; i < str.length(); i++) {
        int val = str.charAt(i);
        if (char_set[val]) return false;
            char_set[val] = true;
        }
        return true;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)