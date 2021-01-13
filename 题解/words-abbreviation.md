# 单词缩写
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/words-abbreviation/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一组 n 个不同的非空字符串，您需要按以下规则为每个单词生成 **最小** 的缩写。
1. 从第一个字符开始，然后加上中间缩写掉的字符的长度，后跟最后一个字符。
2. 如果有冲突，就是多个单词共享相同的缩写，使用较长的前缀，而不是仅使用第一个字符，直到使单词的缩写的映射变为唯一。 换句话说，最终得到的缩写不能映射到多个原始单词。
3. 如果缩写不会使单词更短，则不进行缩写，保持原样。
 ### 样例说明
 
 ### 参考代码
 map自动排序，判断重复。
重复则缩写的位数 --，直到不重复
不重复则判断是否进行缩写。
```java
public class Solution {
    /**
     * @param dict an array of n distinct non-empty strings
     * @return an array of minimal possible abbreviations for every word
     */
    public String[] wordsAbbreviation(String[] dict) {
        // Write your code here
        if (dict == null || dict.length == 0) {
            return new String[0];
        }

        int n = dict.length;
        String[] res = new String[n];
        List<Integer> results = new ArrayList<Integer>();
        for (int i = 0; i < dict.length; i++) {
            results.add(i);
        }
        int len = 2;
        while (!results.isEmpty()) {
            Map<String, Set<Integer>> map = new HashMap<String, Set<Integer>>();
            for (int i : results) {
                String curr = dict[i];
                String abbr = curr.length() <= (len + 1) ?
                    curr : curr.substring(0, len - 1) + (curr.length() - len) + curr.charAt(curr.length() - 1);
                if (map.containsKey(abbr)) {
                    map.get(abbr).add(i);
                } else {
                    Set<Integer> set = new HashSet<Integer>();
                    set.add(i);
                    map.put(abbr, set);
                }
            }
            
            List<Integer> next = new ArrayList<Integer>();
            for (String word : map.keySet()) {
                if (map.get(word).size() == 1) {
                    int index = -1;
                    for (int i : map.get(word)) {
                        index = i;
                    }
                    res[index] = word;
                } else {
                    for (int i : map.get(word)) {
                        next.add(i);
                    }
                }
            }
            results = next;
            len++;
        }
        return res;
    }
}

// version: 高频题班

public class Solution {
    /**
     * @param dict an array of n distinct non-empty strings
     * @return an array of minimal possible abbreviations for every word
     */
    public String[] wordsAbbreviation(String[] dict) {
        int len = dict.length;
        String[] ans = new String[len];
        int[] prefix = new int[len];
        Map<String, Integer> count = new HashMap<>();

        for (int i = 0; i < len; i++) {
            prefix[i] = 1;
            ans[i] = getAbbr(dict[i], 1);
            count.put(ans[i], count.getOrDefault(ans[i], 0) + 1);
        }

        while (true) {
            boolean unique = true;
            for (int i = 0; i < len; i++) {
                if (count.get(ans[i]) > 1) {
                    prefix[i]++;
                    ans[i] = getAbbr(dict[i], prefix[i]);
                    count.put(ans[i], count.getOrDefault(ans[i], 0) + 1);
                    unique = false;
                }
            }
            if (unique) {
                break;
            }
        }
        return ans;
    }

    String getAbbr(String s, int p) {
        if (p >= s.length() - 2) {
            return s;
        }
        String ans;
        ans = s.substring(0, p) + (s.length() - 1 - p) + s.charAt(s.length() - 1);
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)