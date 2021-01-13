# 子串字谜
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-all-anagrams-in-a-string/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串 `s` 和一个 **非空字符串** `p` ，找到在 `s` 中所有关于 `p` 的字谜的起始索引。
字符串仅由小写英文字母组成，字符串 **s** 和 **p** 的长度不得大于 40,000。
输出顺序无关紧要。
 ### 样例说明
 **样例 1:**
```
输入 : s = "cbaebabacd", p = "abc"
输出 : [0, 6]
说明 : 
子串起始索引 index = 0 是 "cba"，是"abc"的字谜。
子串起始索引 index = 6 是 "bac"，是"abc"的字谜。
```
 ### 参考代码
 由于和顺序无关，所以可以开一个数组来记录每个字符的个数，一旦满足p串的字符出现个数，就记录答案。
```java
public class Solution {
    /**
     * @param s a string
     * @param p a non-empty string
     * @return a list of index
     */
    public List<Integer> findAnagrams(String s, String p) {
        // Write your code here
        List<Integer> ans = new ArrayList <Integer>();
        int[] sum = new int[30];

        int plength = p.length(), slength = s.length();
        for(char c : p.toCharArray()){
            sum[c - 'a'] ++;
        }
        
        int start = 0, end = 0, matched = 0;
        while(end < slength){
            if(sum[s.charAt(end) - 'a'] >= 1){
                matched ++;
            }
            sum[s.charAt(end) - 'a'] --;
            end ++;
            if(matched == plength) {
                ans.add(start);
            }
            if(end - start == plength){
                if(sum[s.charAt(start) - 'a'] >= 0){
                    matched --;
                }
                sum[s.charAt(start) - 'a'] ++;
                start ++;
            }
        }
        return ans;
    }
}

//version 高频题班
public class Solution {

    public List<Integer> findAnagrams(String s, String p) {
        // Write your code here
        List<Integer> ans = new ArrayList<>();
        if (s.length() < p.length()) {
            return ans;
        }
        char[] sc = s.toCharArray();
        char[] pc = p.toCharArray();

        int[] det = new int[256];

        for (int i = 0; i < p.length(); i++) {
            det[pc[i]]--;
            det[sc[i]]++;
        }

        int absSum = 0;
        for (int item : det) {
            absSum += Math.abs(item);
        }
        if (absSum == 0) {
            ans.add(0);
        }

        for (int i = p.length(); i < s.length(); i++) {
            int r = sc[i];
            int l = sc[i - p.length()];
            absSum = absSum - Math.abs(det[r]) - Math.abs(det[l]);

            det[r]++;
            det[l]--;

            absSum = absSum + Math.abs(det[r]) + Math.abs(det[l]);
            if (absSum == 0) {
                ans.add(i - p.length() + 1);
            }
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)