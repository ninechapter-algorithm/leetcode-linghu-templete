# 第一个独特字符位置
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/first-position-unique-character/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个字符串。找到字符串中第一个不重复的字符然后返回它的下标。如果不存在这样的字符，返回 `-1`。
 ### 样例说明
 **样例 1:**
```
输入 : s = "lintcode"
输出 : 0
```
**样例 2:**
```
输入 : s = "lovelintcode"
输出 : 2
```
 ### 参考代码
 先将所有字符扫一遍，保存出现过的字符，然后再扫一遍，遇到第一个出现一次的字符就是答案。
```java
public class Solution {
    /**
     * @param s a string
     * @return it's index
     */
    public int firstUniqChar(String s) {
        // Write your code here
        int[] alp = new int[256];
        char[] arr =s.toCharArray();

        for(char c : arr ){
            alp[c]++;
        }

        for(int i = 0; i < arr.length; i++){
            if (alp[arr[i]]==1) return i;
        }

        return -1;
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param s a string
     * @return it's index
     */
    public int firstUniqChar(String s) {
        // Write your code here
        int[] cnt = new int[256];

        for (char c : s.toCharArray()) {
            cnt[c]++;
        }

        for (int i = 0; i < s.length(); i++) {
            if (cnt[s.charAt(i)] == 1) {
                return i;
            }
        }
        return -1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)