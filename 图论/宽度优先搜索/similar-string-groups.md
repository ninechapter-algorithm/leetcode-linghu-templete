# 相似字符串组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/similar-string-groups/?utm_source=sc-github-wzz)
 ## 题目描述
 如果我们交换字符串 X 中的两个不同位置的字母，使得它和字符串 Y 相等，那么称 X 和 Y 两个字符串相似。

例如，"tars" 和 "rats" 是相似的 (交换 0 与 2 的位置)； "rats" 和 "arts" 也是相似的，但是 "star" 不与 "tars"，"rats"，或 "arts" 相似。

总之，它们通过相似性形成了两个关联组：{"tars", "rats", "arts"} 和 {"star"}。注意，"tars" 和 "arts" 是在同一组中，即使它们并不相似。形式上，对每个组而言，要确定一个单词在组中，只需要这个词和该组中至少一个单词相似。

我们给出了一个不包含重复的字符串列表 A。列表中的每个字符串都是 A 中其它所有字符串的一个字母异位词。请问 A 中有多少个相似字符串组？
 ### 样例说明
 **样例 1:**
```
输入: ["tars","rats","arts","star"]
输出: 2
```

**样例 2:**
```
输入: ["omv","ovm"]
输出:1
```
 ### 参考代码
 找连通块的个数。BFS 也可以做。
只需要 for 每个单词，从每个单词出发标记 相似单词，看看一共标记几次即可。
这里有一个 tricky 的地方是，在找相似单词的时候，有两种做法：
- 做法1: 交换两个位置，然后看看在 wordSet 里有没有出现 $O(L^3)$
- 做法2: for wordSet 里的每个单词看看字符不同的位置是不是 2 个 $O(NL)$

其中 N 是单词个数，L是单词长度，这两个方法不一定哪个好，可以比较 $N$ 和 $L^2$ 的大小来决定使用哪个。

```
[[python]]
class Solution:
    def numSimilarGroups(self, strs):
        word_set = set(strs)
        visited = set()
        
        similar_set = 0
        for word in strs:
            if word in visited:
                continue
            similar_set += 1
            self.mark_similar_set(word, word_set, visited)
        
        return similar_set
        
    def mark_similar_set(self, word, word_set, visited):
        from collections import deque
        queue = deque([word])
        visited.add(word)
        while queue:
            word = queue.popleft()
            for neighbor in self.get_neighbor_words(word, word_set):
                if neighbor in visited:
                    continue
                queue.append(neighbor)
                visited.add(neighbor)
        
    def get_neighbor_words(self, word, word_set):
        if len(word) ** 2 < len(word_set):
            return self.get_neighbor_words1(word, word_set)
        return self.get_neighbor_words2(word, word_set)
        
    def get_neighbor_words1(self, word, word_set):
        # O(L^3)
        n = len(word)
        chars = list(word)
        neighbor_words = []
        for i in range(n):
            for j in range(i + 1, n):
                chars[i], chars[j] = chars[j], chars[i]
                anagram = ''.join(chars)
                if anagram in word_set:
                    neighbor_words.append(anagram)
                chars[i], chars[j] = chars[j], chars[i]
        return neighbor_words    

    def get_neighbor_words2(self, word, word_set):
        # O(N*L)
        neighbors = []
        for neighbor in word_set:
            if self.is_similar(word, neighbor):
                neighbors.append(neighbor)
        return neighbors

    def is_similar(self, word1, word2):
        diff = 0
        for c1, c2 in zip(word1, word2):
            if c1 != c2:
                diff += 1
        return diff == 2
[[java]]
public class Solution {
    /**
     * @param A: a string array
     * @return: the number of groups 
     */
    public int numSimilarGroups(String[] strs) {
        Set<String> wordSet = new HashSet<>();
        Set<String> visited = new HashSet<>();
        for (int i = 0; i < strs.length; i++) {
            wordSet.add(strs[i]);
        }
        
        int similarSet = 0;
        for (String word : strs) {
            if (visited.contains(word)) {
                continue;
            }
            similarSet += 1;
            markSimilarSet(word, wordSet, visited);
        }
        
        return similarSet;
    }
    
    private void markSimilarSet(String word, Set<String> wordSet, Set<String> visited) {
        Queue<String> queue = new ArrayDeque<>();
        queue.offer(word);
        visited.add(word);
        while (!queue.isEmpty()) {
           word = queue.poll();
            for (String neighbor : getNeighborWords(word, wordSet)) {
                if (visited.contains(neighbor)) {
                    continue;
                }
                queue.offer(neighbor);
                visited.add(neighbor);
            }
        }
    }
    
    private List<String> getNeighborWords(String word, Set<String> wordSet) {
        if (word.length() * word.length() < wordSet.size()) {
            return getNeighborWords1(word, wordSet);
        } 
        return getNeighborWords2(word, wordSet);
    }
    
    private List<String> getNeighborWords1(String word, Set<String> wordSet) {
        int n = word.length();
        char[] chars = word.toCharArray();
        List<String> neighbors = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                char temp = chars[i];
                chars[i] = chars[j];
                chars[j] = temp;
                String anagram = String.valueOf(chars);
                if (wordSet.contains(anagram)) {
                    neighbors.add(anagram);
                }
                temp = chars[i];
                chars[i] = chars[j];
                chars[j] = temp;
            }
        }
        
        return neighbors;
    }
    
    private List<String> getNeighborWords2(String word, Set<String> wordSet) {
        List<String> neighbors = new ArrayList<>();
        for (String neighbor : wordSet) {
            if (isSimilar(word, neighbor)) {
                neighbors.add(neighbor);
            }
        }
        
        return neighbors;
    }
    
    private boolean isSimilar(String word1, String word2) {
        int diff = 0;
        for (int i = 0; i < word1.length(); i++) {
            if (word1.charAt(i) != word2.charAt(i)) {
                diff++;
            }
        }
        
        return diff == 2;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)