# 包含所有单词连接的子串
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/substring-with-concatenation-of-all-words/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一个字符串`s`和一个单词列表`words`，`words`里的单词的长度都相同。 在`s`中查找子串的所有起始索引，这个子串是`words`中每个单词恰好一次的连接，且没有任何插入字符。
 ### 样例说明
 
 ### 参考代码
 复杂度：$O(nm)$

$n = len(s),m =  len(words[0]), k = len(words)$

暴力做法，枚举开始位置，判断之后长度$m*k$的子串是否由给定字符串集合组成，最坏复杂度为$O(nmk)$。

对于长度为$m$的字符串，0与m位置开始的区别，只在于少了$s[0:m]$，多了$s[m*k+1:(m+1)*k]$，所以产生了许多冗余操作。我们根据开始位置$0$ ~ $m-1$分类，扫描字符串`s`，使用一个滑动窗口记录当前匹配了那些字符串，当下一个字符串不在`words`中，清空窗口(任意包含该串的均不合法)，如果记录的出现次数超过了`words`中数量，表示需要滑动窗口，

窗口中单词数量等于k时，更新答案。
```java
public class Solution {
    public ArrayList<Integer> findSubstring(String S, String[] L) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        HashMap<String, Integer> toFind = new HashMap<String, Integer>();
        HashMap<String, Integer> found = new HashMap<String, Integer>();
        int m = L.length, n = L[0].length();
        for (int i = 0; i < m; i ++){
            if (!toFind.containsKey(L[i])){
                toFind.put(L[i], 1);
            }
            else{
                toFind.put(L[i], toFind.get(L[i]) + 1);
            }
        }
        for (int i = 0; i <= S.length() - n * m; i ++){
            found.clear();
            int j;
            for (j = 0; j < m; j ++){
                int k = i + j * n;
                String stub = S.substring(k, k + n);
                if (!toFind.containsKey(stub)) break;
                if(!found.containsKey(stub)){
                    found.put(stub, 1);
                }
                else{
                    found.put(stub, found.get(stub) + 1);
                }
                if (found.get(stub) > toFind.get(stub)) break;
            }
            if (j == m) result.add(i);
        }
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)