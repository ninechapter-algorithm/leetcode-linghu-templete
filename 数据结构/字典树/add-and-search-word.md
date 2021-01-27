# 单词的添加与查找
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/add-and-search-word/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一个包含下面两个操作的数据结构：`addWord(word)`, `search(word)`

`addWord(word)`会在数据结构中添加一个单词。而`search(word)`则支持普通的单词查询或是只包含`.`和`a-z`的简易正则表达式的查询。

一个 `.` 可以代表一个任何的字母。
 ### 样例说明
 
 ### 参考代码
 可以说, 这道题是 [442. 实现 Trie (前缀树)](https://www.lintcode.com/problem/implement-trie-prefix-tree/description) 的升级版.

只需要在查询的时候将 `'.'` 处理为回溯即可, 即遇到 `'.'` 则需要访问每一个子节点判断是否有匹配.
```java
// Version1 use Array
class TrieNode {

    public TrieNode[] children;
    public boolean hasWord;
    
    public TrieNode() {
        children = new TrieNode[26];
        for (int i = 0; i < 26; ++i)
            children[i] = null;
        hasWord = false;
    }
}


public class WordDictionary {
    private TrieNode root;
 
    public WordDictionary() {
        root = new TrieNode();
    }
 
    // Adds a word into the data structure.
    public void addWord(String word) {
        TrieNode now = root;
        for (int i = 0; i < word.length(); i++) {
            Character c = word.charAt(i);
            if (now.children[c - 'a'] == null) {
                now.children[c - 'a'] = new TrieNode();
            }
            now = now.children[c - 'a'];
        }
        now.hasWord = true;
    }
    
    boolean find(String word, int index, TrieNode now) {
        if (index == word.length()) {
            return now.hasWord;
        }
        
        Character c = word.charAt(index);
        if (c == '.') {
            for (int i = 0; i < 26; ++i) 
                if (now.children[i] != null) {
                    if (find(word, index+1, now.children[i]))
                        return true;
                }
            return false;
        } else if (now.children[c - 'a'] != null) {
            return find(word, index+1, now.children[c - 'a']);  
        } else {
            return false;
        }
    }
    
    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        // Write your code here
        return find(word, 0, root);
    }
}

// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");



// Version 2 use HashMap and dfs
class TrieNode {
    // Initialize your data structure here.
    public HashMap<Character, TrieNode> children;
    public boolean hasWord;
    
    // Initialize your data structure here.
    public TrieNode() {
        children = new HashMap<Character, TrieNode>();
        hasWord = false;
    }
}


public class WordDictionary {
    private TrieNode root;
 
    public WordDictionary() {
        root = new TrieNode();
    }
 
    // Adds a word into the data structure.
    public void addWord(String word) {
        TrieNode now = root;
        for (int i = 0; i < word.length(); i++) {
            Character c = word.charAt(i);
            if (!now.children.containsKey(c)) {
                now.children.put(c, new TrieNode());
            }
            now = now.children.get(c);
        }
        now.hasWord = true;
    }
    
    boolean find(String word, int index, TrieNode now) {
        if (index == word.length()){
            if (now.children.size() == 0) 
                return true; 
            else
                return false;
        }
        
        Character c = word.charAt(index);
        if (now.children.containsKey(c)) {
            if (index == word.length()-1 && now.children.get(c).hasWord) {
                return true;
            }
            return find(word, index+1, now.children.get(c)) ;  
        } else if(c == '.') {
            boolean result = false;
            for (Map.Entry<Character, TrieNode> child: now.children.entrySet()) {
                if (index == word.length()-1 && child.getValue().hasWord) {
                    return true;
                } 
 
                //if any path is true, set result to be true; 
                if (find(word, index+1, child.getValue())) {
                    result = true;
                }
            }
            return result;
        } else {
            return false;
        }
    }
    
    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        // Write your code here
        return find(word, 0, root);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)