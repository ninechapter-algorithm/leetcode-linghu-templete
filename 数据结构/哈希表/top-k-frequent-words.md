# 最高频的K个单词
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/top-k-frequent-words/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个单词列表，求出这个列表中出现频次最高的K个单词。
 ### 样例说明
 **样例 1:**

```
输入:
  [
    "yes", "lint", "code",
    "yes", "code", "baby",
    "you", "baby", "chrome",
    "safari", "lint", "code",
    "body", "lint", "code"
  ]
  k = 3
输出: ["code", "lint", "baby"]
```

**样例 2:**

```
输入:
  [
    "yes", "lint", "code",
    "yes", "code", "baby",
    "you", "baby", "chrome",
    "safari", "lint", "code",
    "body", "lint", "code"
  ]
  k = 4
输出: ["code", "lint", "baby", "yes"] 
```
 ### 参考代码
 欲记录单词出现的次数, 首选是哈希表. 大多高级语言内置相关的数据结构, 编码简单.

使用哈希表记录每个单词出现的次数, 然后需要将单词按照 次数(主要关键词)和字典序(次要关键字) 排序, 取出前k个即可.

排序的过程可以用 heap, 也可以使用快排等排序算法.
```java
class Pair {
    String key;
    int value;
    
    Pair(String key, int value) {
        this.key = key;
        this.value = value;
    }
}

public class Solution {
    /**
     * @param words an array of string
     * @param k an integer
     * @return an array of string
     */
     
    private Comparator<Pair> pairComparator = new Comparator<Pair>() {
        public int compare(Pair left, Pair right) {
            if (left.value != right.value) {
                return left.value - right.value;
            }
            return right.key.compareTo(left.key);
        }
    };
    
    public String[] topKFrequentWords(String[] words, int k) {
        if (k == 0) {
            return new String[0];
        }
        
        HashMap<String, Integer> counter = new HashMap<>();
        for (String word : words) {
            if (counter.containsKey(word)) {
                counter.put(word, counter.get(word) + 1);
            } else {
                counter.put(word, 1);
            }
        }
        
        PriorityQueue<Pair> Q = new PriorityQueue<Pair>(k, pairComparator);
        for (String word : counter.keySet()) {
            Pair peak = Q.peek();
            Pair newPair = new Pair(word, counter.get(word));
            if (Q.size() < k) {
                Q.add(newPair);
            } else if (pairComparator.compare(newPair, peak) > 0) {
                Q.poll();
                Q.add(newPair);
            }
        }
        
        String[] result = new String[k];
        int index = 0;
        while (!Q.isEmpty()) {
            result[index++] = Q.poll().key;
        }
        
        // reverse
        for (int i = 0; i < index / 2; i++) {
            String temp = result[i];
            result[i] = result[index - i - 1];
            result[index - i - 1] = temp;
        }
        
        return result;
     }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)