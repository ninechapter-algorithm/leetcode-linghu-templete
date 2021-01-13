# 字符至少出现K次的最长子串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-substring-with-at-least-k-repeating-characters/?utm_source=sc-github-wzz)
 ## 题目描述
 找出给定字符串的最长子串，使得该子串中的每一个字符都出现了至少k次，返回这个子串的长度。


 ### 样例说明
 **样例1：**
~~~~.
输入：
s = "aaabb", k = 3
输出：
3
解释：
最长子串为"aaa"，因为'a'重复了3次。
~~~~
**样例2：**
~~~~.
输入：
s = "ababbc", k = 2
输出：
5
解释：
最长子串为"ababb"，因为'a'重复了2次，同时'b'重复了3次。
~~~~
 ### 参考代码
 贪心法 + 递归。
如果一个字符出现次数 < k 说明最长的要么在它左边，要么在它右边（不可能跨过他），从它拆开往下递归计算即可。
```java
class Solution {
    public int longestSubstring(String s, int k) {
        HashMap<Character, Integer> counter = getCharCounter(s);
        
        int left = 0;
        int longest = 0;
        for (int i = 0; i < s.length(); i++) {
            if (counter.get(s.charAt(i)) < k) {
                int sub_longest = longestSubstring(s.substring(left, i), k);
                longest = Math.max(longest, sub_longest);
                left = i + 1;
            }
        }
        
        if (left == 0) {
            return s.length();
        }
        
        int sub_longest = longestSubstring(s.substring(left, s.length()), k);
        longest = Math.max(longest, sub_longest);
        
        return longest;
    }
    
    private HashMap<Character, Integer> getCharCounter(String s) {
        HashMap<Character, Integer> counter = new HashMap<>();
        
        for (int i = 0; i < s.length(); i++) {
            Character c = s.charAt(i);
            Integer val = counter.getOrDefault(c, 0);
            counter.put(c, val + 1);
        }
        
        return counter;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)