# 拼字游戏
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/boggle-game/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个2D矩阵包括 `a-z` 和字典 `dict`，找到矩阵上最大的单词集合，这些单词不能在相同的位置重叠。返回最大集合的 `大小`。
 ### 样例说明
 **样例 1:**
```
输入:
["abc","def","ghi"]
{"abc","defi","gh"}
输出:
3

解释:
我们可以得到最大的集合 `["abc", "defi", "gh"]`
```

**样例 2:**
```
输入:
["aaaa","aaaa","aaaa","aaaa"]
{"a"}
输出:
16

解释:
我们可以得到最大的集合 `["a", "a","a","a","a","a","a","a","a","a","a","a","a","a","a","a"]`
```

 ### 参考代码
 tire + dfs。
字典树用于前缀查找。
dfs用于搜索，
找到单词时搜索下一个单词
没有搜索到单词时，四方向遍历（回溯 + 标记）
```java
//建立tire树的过程
class Trie {
    TrieNode root;

    Trie() {
        root = new TrieNode('0');
    }

    public void insert(String word) {
        if(word == null || word.length() == 0) {
            return;
        }
        TrieNode node = root;
        for(int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            if(node.children[ch - 'a'] == null) {
                node.children[ch - 'a'] = new TrieNode(ch);
            }
            node = node.children[ch - 'a'];
        }
        node.isWord = true;
    }
}
//tire的结点
class TrieNode {
    char value;
    boolean isWord;
    TrieNode[] children;

    TrieNode(char v) {
        value = v;
        isWord = false;
        children = new TrieNode[26];
    }
}

public class Solution {
    /**
     * @param board a list of lists of character
     * @param words a list of string
     * @return an integer
     */
    public int boggleGame(char[][] board, String[] words) {
        // Write your code here
        Trie trie = new Trie();
        for(String word : words) {
            trie.insert(word);
        }

        int m = board.length;
        int n = board[0].length;
        List<String> result = new ArrayList<>();
        boolean[][] visited = new boolean[m][n];
        List<String> path = new ArrayList<>();
        findWords(result, board, visited, path, 0, 0, trie.root);
        return result.size();
    }
	//从当前位置出发寻单词存不存在
    public void findWords(List<String> result, char[][] board, boolean[][] visited, List<String> words, int x, int y, TrieNode root) {

        int m = board.length;
        int n = board[0].length;

        for (int i = x; i < m; i++) {
            for (int j = y; j < n; j++) {
                List<List<Integer>> nextWordIndexes = new ArrayList<>();
                List<Integer> path = new ArrayList<>();
                getNextWords(nextWordIndexes, board, visited, path, i, j, root);
                for (List<Integer> indexes : nextWordIndexes) {
                    String word = "";
                    for (int index : indexes) {
                        int row = index / n;
                        int col = index % n;
                        visited[row][col] = true;
                        word += board[row][col];
                    }

                    words.add(word);
                    if (words.size() > result.size()) {
                        result.clear();
                        result.addAll(words);
                    }
                    findWords(result, board, visited, words, i, j, root);
                    for (int index : indexes) {
                        int row = index / n;
                        int col = index % n;
                        visited[row][col] = false;
                    }
                    words.remove(words.size() - 1);
                }
            }
            y = 0;
        }
    }
    
    int []dx = {0, 1, 0, -1};
    int []dy = {1, 0, -1, 0};
    //dfs搜索查找单词
    private void getNextWords(List<List<Integer>> words, char[][] board,
                              boolean[][] visited, List<Integer> path, int i, int j, TrieNode root) {
        if(i < 0 | i >= board.length || j < 0 || j >= board[0].length
            || visited[i][j] == true || root.children[board[i][j] - 'a'] == null) {
            return;
        }
		//找下一个单词
        root = root.children[board[i][j] - 'a'];
        if(root.isWord) {
            List<Integer> newPath = new ArrayList<>(path);
            newPath.add(i * board[0].length + j);
            words.add(newPath);
            return;
        }
		//回溯标记
        visited[i][j] = true;
        path.add(i * board[0].length + j);
        for (int k = 0; k < 4; k ++) {
            getNextWords(words, board, visited, path, i + dx[k], j + dy[k], root);
        }
        path.remove(path.size() - 1);
        visited[i][j] = false;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)