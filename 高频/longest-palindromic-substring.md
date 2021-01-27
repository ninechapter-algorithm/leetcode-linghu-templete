# 最长回文子串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-palindromic-substring/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个字符串（假设长度最长为1000），求出它的最长回文子串，你可以假定只有一个满足条件的最长回文串。
 ### 样例说明
 **样例 1:**
```
输入:"abcdzdcab"
输出:"cdzdc"
```
**样例 2:**
```
输入:"aba"
输出:"aba"
```
 ### 参考代码
 基于中心点枚举的算法，时间复杂度 O(n^2)
```
[[java]]
public class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }
        
        int start = 0, len = 0, longest = 0;
        for (int i = 0; i < s.length(); i++) {
            len = findLongestPalindromeFrom(s, i, i);
            if (len > longest) {
                longest = len;
                start = i - len / 2;
            }
            
            len = findLongestPalindromeFrom(s, i, i + 1);
            if (len > longest) {
                longest = len;
                start = i - len / 2 + 1;
            }
        }
        
        return s.substring(start, start + longest);
    }
    
    private int findLongestPalindromeFrom(String s, int left, int right) {
        int len = 0;
        while (left >= 0 && right < s.length()) {
            if (s.charAt(left) != s.charAt(right)) {
                break;
            }
            len += left == right ? 1 : 2;
            left--;
            right++;
        }
        
        return len;
    }
}
[[python]]
class Solution:
    def longestPalindrome(self, s):
        if not s:
            return ""
            
        answer = (0, 0)
        for mid in range(len(s)):
            answer = max(answer, self.get_palindrom_from(s, mid, mid))
            answer = max(answer, self.get_palindrom_from(s, mid, mid + 1))
        
        return s[answer[1]: answer[0] + answer[1]]    
        
    def get_palindrom_from(self, s, left, right):
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return (right - left - 1, left + 1)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)