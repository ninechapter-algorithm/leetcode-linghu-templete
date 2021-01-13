# 最长无重复字符的子串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-substring-without-repeating-characters/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串，请找出其中无重复字符的最长子字符串。
 ### 样例说明
 **样例 1:**

```
输入: "abcabcbb"
输出: 3
解释: 最长子串是 "abc".
```

**样例 2:**

```
输入: "bbbbb"
输出: 1
解释: 最长子串是 "b".
```
 ### 参考代码
 枚举, 记录每一个字母上一次出现的位置.
 
 再设定一个左边界, 到当前枚举到的位置之间的字符串为不含重复字符的子串.
 
 若新碰到的字符的上一次的位置在左边界右边, 则需要向右移动左边界, 枚举的过程中取最大值即可.
```java
public class Solution {
    /**
     * @param s: a string
     * @return: an integer 
     */
     //方法一：
    public int lengthOfLongestSubstring(String s) {
        int[] map = new int[256]; // map from character's ASCII to its last occured index
        
        int j = 0;
        int i = 0;
        int ans = 0;
        for (i = 0; i < s.length(); i++) {
            while (j < s.length() && map[s.charAt(j)]==0) {
                map[s.charAt(j)] = 1;
                ans = Math.max(ans, j-i + 1);
                j ++;
            }
            map[s.charAt(i)] = 0;
        }
        
        return ans;
    }
}


public class Solution {
    /**
     * @param s: a string
     * @return: an integer
     */
    public int lengthOfLongestSubstring(String s) {
        // write your code here
        int[] cnt = new int[256];
        char[] sc = s.toCharArray();

        int ans = 0;
        for (int l = 0, r = 0; r < s.length(); r++) {
            cnt[sc[r]]++;
            while (cnt[sc[r]] > 1) {
                cnt[sc[l]]--;
                l++;
            }
            ans = Math.max(ans, r - l + 1);
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)