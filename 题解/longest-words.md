# 最长单词
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/longest-words/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个词典，找出其中所有最长的单词。
 ### 样例说明
 
 ### 参考代码
 ```java
class Solution {
    /**
     * @param dictionary: an array of strings
     * @return: an arraylist of strings
     */
    ArrayList<String> longestWords(String[] dictionary) {
        // write your code here
        int maxLen = 0;
        ArrayList<String> ans = new ArrayList<String>();
        for (int i=0; i<dictionary.length; ++i) 
            if (dictionary[i].length()>maxLen) maxLen = dictionary[i].length();
        for (int i=0; i<dictionary.length; ++i)
            if (dictionary[i].length()==maxLen) ans.add(dictionary[i]);
        return ans;
    }
};

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)