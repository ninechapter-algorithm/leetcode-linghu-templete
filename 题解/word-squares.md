# 单词矩阵
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/word-squares/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一系列 **不重复的单词**，找出所有用这些单词能构成的 [单词矩阵](https://en.wikipedia.org/wiki/Word_square "Word square")。
一个有效的单词矩阵是指, 如果从第 k 行读出来的单词和第 k 列读出来的单词相同(0 <= k < max(numRows, numColumns))，那么就是一个单词矩阵.
例如，单词序列为 `["ball","area","lead","lady"]` ,构成一个单词矩阵。因为对于每一行和每一列，读出来的单词都是相同的。
```
b a l l
a r e a
l e a d
l a d y
```
 ### 样例说明
 **样例 1:**
```
输入:
["area","lead","wall","lady","ball"]
输出:
[["wall","area","lead","lady"],["ball","area","lead","lady"]]

解释:
输出包含 两个单词矩阵，这两个矩阵的输出的顺序没有影响(只要求矩阵内部有序)。
```

**样例 2:**
```
输入:
["abat","baba","atan","atal"]
输出:
 [["baba","abat","baba","atan"],["baba","abat","baba","atal"]]
```
 ### 参考代码
 字典树+dfs。
根据已添加单词确定下一个单词的前缀，利用dfs搜索。
```java
public class Solution {
     class TrieNode {
        List<String> startWith;
        TrieNode[] children;

        TrieNode() {
            startWith = new ArrayList<>();
            children = new TrieNode[26];
        }
    }

    class Trie {
        TrieNode root;

        Trie(String[] words) {
            root = new TrieNode();
            for (String w : words) {
                TrieNode cur = root;
                for (char ch : w.toCharArray()) {
                    int idx = ch - 'a';
                    if (cur.children[idx] == null)
                        cur.children[idx] = new TrieNode();
                    cur.children[idx].startWith.add(w);
                    cur = cur.children[idx];
                }
            }
        }

        List<String> findByPrefix(String prefix) {
            List<String> ans = new ArrayList<>();
            TrieNode cur = root;
            for (char ch : prefix.toCharArray()) {
                int idx = ch - 'a';
                if (cur.children[idx] == null)
                    return ans;

                cur = cur.children[idx];
            }
            ans.addAll(cur.startWith);
            return ans;
        }
    }

    public List<List<String>> wordSquares(String[] words) {
        List<List<String>> ans = new ArrayList<>();
        if (words == null || words.length == 0)
            return ans;
        int len = words[0].length();
        Trie trie = new Trie(words);
        List<String> ansBuilder = new ArrayList<>();
        for (String w : words) {
            ansBuilder.add(w);
            search(len, trie, ans, ansBuilder);
            ansBuilder.remove(ansBuilder.size() - 1);
        }

        return ans;
    }

    private void search(int len, Trie tr, List<List<String>> ans,
            List<String> ansBuilder) {
        if (ansBuilder.size() == len) {
            ans.add(new ArrayList<>(ansBuilder));
            return;
        }

        int idx = ansBuilder.size();
        StringBuilder prefixBuilder = new StringBuilder();
        for (String s : ansBuilder)
            prefixBuilder.append(s.charAt(idx));
        List<String> startWith = tr.findByPrefix(prefixBuilder.toString());
        for (String sw : startWith) {
            ansBuilder.add(sw);
            search(len, tr, ans, ansBuilder);
            ansBuilder.remove(ansBuilder.size() - 1);
        }
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param words a set of words without duplicates
     * @return all word squares
     */

    void initPrefix(String[] words, Map<String, List<String>> hash) {
        for (String item : words) {
            hash.putIfAbsent("", new ArrayList<>());
            hash.get("").add(item);

            String prefix = "";
            for (char c : item.toCharArray()) {
                prefix += c;
                hash.putIfAbsent(prefix, new ArrayList<>());
                hash.get(prefix).add(item);
            }
        }
    }

    boolean checkPrefix(int l, String nextWord, int wordLen, Map<String, List<String>> hash, List<String> squares) {
        for (int j = l + 1; j < wordLen; j++) {
            String prefix = "";
            for (int k = 0; k < l; k++) {
                prefix += squares.get(k).charAt(j);
            }
            prefix += nextWord.charAt(j);
            if (!hash.containsKey(prefix)) {
                return false;
            }
        }
        return true;
    }

    void dfs(int l, int wordLen, Map<String, List<String>> hash, List<String> squares, List<List<String>> ans) {
        if (l == wordLen) {
            ans.add(new ArrayList<>(squares));
            return;
        }
        String prefix = "";
        for (int i = 0; i < l; i++) {
            prefix += squares.get(i).charAt(l);
        }

        for (String item : hash.get(prefix)) {
            if (!checkPrefix(l, item, wordLen, hash, squares)) {
                continue;
            }
            squares.add(item);
            dfs(l + 1, wordLen, hash, squares, ans);
            squares.remove(squares.size() - 1);
        }
    }

    public List<List<String>> wordSquares(String[] words) {
        // Write your code here
        List<List<String>> ans = new ArrayList<>();
        if (words.length == 0) {
            return ans;
        }
        Map<String, List<String>> hash = new HashMap<>();
        initPrefix(words, hash);

        List<String> squares = new ArrayList<>();
        dfs(0, words[0].length(), hash, squares, ans);
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)