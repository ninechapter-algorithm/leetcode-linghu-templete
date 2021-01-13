# 推多米诺
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/push-dominoes/?utm_source=sc-github-wzz)
 ## 题目描述
 432
 ### 样例说明
 432
 ### 参考代码
 BFS解法
```
[[python]]
class Solution:
    """
    @param dominoes: a string
    @return: a string representing the final state
    """
    def pushDominoes(self, dominoes):
        queue = []
        dominoes = list(dominoes)
        for index, c in enumerate(dominoes):
            if c != '.':
                queue.append((index, c))
        
        while queue:
            falling = {}
            for (index, c) in queue:
                if c == 'L' and index > 0 and dominoes[index - 1] == '.':
                    if index - 1 in falling:
                        falling[index - 1] = '.'
                    else:
                        falling[index - 1] = 'L'
                if c == 'R' and index + 1 < len(dominoes) and dominoes[index + 1] == '.':
                    if index + 1 in falling:
                        falling[index + 1] = '.'
                    else:
                        falling[index + 1] = 'R'
            queue = []
            for index, c in falling.items():
                if c != '.':
                    queue.append((index, c))
                    dominoes[index] = c
        
        return ''.join(dominoes)
[[java]]
class IndexValuePair {
    int index;
    char value;
    public IndexValuePair(int index, char value) {
        this.index = index;
        this.value = value;
    }
}

public class Solution {
    /**
     * @param dominoes: a string
     * @return: a string representing the final state
     */
    public String pushDominoes(String dominoes) {
        List<IndexValuePair> queue = new ArrayList<>();
        char[] chars = dominoes.toCharArray();
        for (int index = 0; index < chars.length; index++) {
            if (chars[index] != '.') {
                queue.add(new IndexValuePair(index, chars[index]));
            }
        }
        
        while (!queue.isEmpty()) {
            Map<Integer, Character> falling = new HashMap<>();
            for (IndexValuePair pair: queue) {
                int index = pair.index, value = pair.value;
                if (value == 'L' && index > 0 && chars[index - 1] == '.') {
                    if (falling.containsKey(index - 1)) {
                        falling.put(index - 1, '.');
                    } else {
                        falling.put(index - 1, 'L');
                    }
                }
                if (value == 'R' && index + 1 < chars.length && chars[index + 1] == '.') {
                    if (falling.containsKey(index + 1)) {
                        falling.put(index + 1, '.');
                    } else {
                        falling.put(index + 1, 'R');
                    }
                }
            }
            queue = new ArrayList<>();
            for (int index: falling.keySet()) {
                char value = falling.get(index);
                if (value != '.') {
                    queue.add(new IndexValuePair(index, value));
                    chars[index] = value;
                }
            }
        }
        return String.valueOf(chars);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)