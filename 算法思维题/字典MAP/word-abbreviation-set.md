# 单词缩写集
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/word-abbreviation-set/?utm_source=sc-github-wzz)
 ## 题目描述
 一个单词的缩写根据以下的形式。下面是一些缩写的例子
```
a) it                      --> it    (没有缩写)

     1
b) d|o|g                   --> d1g

              1    1  1
     1---5----0----5--8
c) i|nternationalizatio|n  --> i18n

              1
     1---5----0
d) l|ocalizatio|n          --> l10n
```
假设你有一个字典和给你一个单词，判断这个单词的缩写在字典中是否是唯一的。当字典中的**其他单词的缩写**均与它不同的时候， 这个单词的缩写是唯一的.
 ### 样例说明
 
 ### 参考代码
 判断待查找的单词在字典中出现的次数是否和缩写在缩写字典中出现的次数一样
```java
public class ValidWordAbbr {

    private Map<String,Set<String>> d;

    // @param dictionary a list of word
    public ValidWordAbbr(String[] dictionary) {
        // Write your code here
        d = new HashMap<String, Set<String>>();
        for (int i = 0;i < dictionary.length; i++) {
            String w = dictionary[i];
            String abbr = getAbbr(w); 
        
            if (d.containsKey(abbr)) {
                Set<String> s = d.get(abbr);
                if (!s.contains(w)) s.add(w);
            } else {
                Set<String> s = new HashSet<String>();
                s.add(w);
                d.put(abbr,s);
            }
        }
    }

    /**
     * @param word a string
     * @return true if its abbreviation is unique or false
     */
    public boolean isUnique(String word) {
        // Write your code here
        String a = getAbbr(word);
        if (d.containsKey(a)) {
            Set<String> s = d.get(a);
            if (s.size() == 1 && s.contains(word)) {
                return true;
            } else {
                return false;
            }
        } else {
            return true;
        }
    }

    private String getAbbr(String w){
        int len = w.length() - 2;
        if (len <= 0) {
            return w;
        }
        return "" + w.charAt(0) + len + w.charAt(w.length() - 1);
    }
}

/**
 * Your ValidWordAbbr object will be instantiated and called as such:
 * ValidWordAbbr obj = new ValidWordAbbr(dictionary);
 * boolean param = obj.isUnique(word);
 */



// version: 高频题班
public class ValidWordAbbr {
    Map<String, Integer> dict = new HashMap<>();
    Map<String, Integer> abbr = new HashMap<>();

    // @param dictionary a list of word
    public ValidWordAbbr(String[] dictionary) {
        // Write your code here
        for (String d : dictionary) {
            dict.put(d, dict.getOrDefault(d, 0) + 1);
            String a = getAbbr(d);
            abbr.put(a, abbr.getOrDefault(a, 0) + 1);
        }
    }
    /**
     * @param word a string
     * @return true if its abbreviation is unique or false
     */
    public boolean isUnique(String word) {
        // Write your code here
        String a = getAbbr(word);
        return dict.get(word) == abbr.get(a);
    }

    String getAbbr(String str) {
        if (str.length() <= 2) {
            return str;
        }
        return "" + str.charAt(0) + (str.length() - 2) + str.charAt(str.length() - 1);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)