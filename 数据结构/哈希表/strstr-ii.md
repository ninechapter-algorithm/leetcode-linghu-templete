# 字符串查找 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/strstr-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 实现时间复杂度为 O(n + m)的方法 `strStr`。
`strStr` 返回目标字符串在源字符串中第一次出现的第一个字符的位置. 目标字串的长度为 *m* , 源字串的长度为 *n* . 如果目标字串不在源字串中则返回 -1。
 ### 样例说明
 **样例 1:**
```
输入：source = "abcdef"， target = "bcd"
输出：1
解释：
字符串第一次出现的位置为1。
```


**样例 2:**
```
输入：source = "abcde"， target = "e"
输出：4
解释：
字符串第一次出现的位置为4。
```
 ### 参考代码
 考点：
* hash
* kmp

题解：
* 采用字符串哈希，字符串哈希时需要将字符串映射为数字，hash_target = (hash_target * 33 + target.charAt(i) - 'a') % mod;此处哈希函数，提供了字符串转化数字的关系式。
* 对于需要匹配的子串对应一个值，然后再遍历主串，当前位置为i，则用i的哈希值减去i-m部分的哈希值，求出中间m个长度的子串的哈希值，如果与要匹配串相同，由于哈希本身不安全，需要截取出来m长度的子串再进行匹配，完全相同即可。
* 注意负数取模时，需要通过+mod，将负数变为正数。
* kmp是线性的字符串匹配算法，同样可以实现。
```java
public class Solution {
    /**
     * @param source a source string
     * @param target a target string
     * @return an integer as index
     */
    public int strStr2(String source, String target) {
        if(target == null) {
            return -1;
        }
        int m = target.length();
        if(m == 0 && source != null) {
            return 0;
        }
        
        if(source == null) {
            return -1;
        }
        int n = source.length();
        if(n == 0) {
            return -1;
        }

        // mod could be any big integer
        // just make sure mod * 33 wont exceed max value of int.
        int mod = Integer.MAX_VALUE / 33;
        int hash_target = 0;

        // 33 could be something else like 26 or whatever you want
        for (int i = 0; i < m; ++i) {
            hash_target = (hash_target * 33 + target.charAt(i) - 'a') % mod;
            if (hash_target < 0) {
                hash_target += mod;
            }
        }

        int m33 = 1;
        for (int i = 0; i < m - 1; ++i) {
            m33 = m33 * 33 % mod;
        }

        int value = 0;
        for (int i = 0; i < n; ++i) {
            if (i >= m) {
                value = (value - m33 * (source.charAt(i - m) - 'a')) % mod;
            }

            value = (value * 33 + source.charAt(i) - 'a') % mod;
            if (value < 0) {
                value += mod;
            }

            if (i >= m - 1 && value == hash_target) {
                // you have to double check by directly compare the string
                if (target.equals(source.substring(i - m + 1, i + 1))) {
                    return i - m + 1;
                }
            }
        }
        return -1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)