# 最常使用的K个单词II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/top-k-frequent-words-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 在实时数据流中找到最常使用的k个单词.
实现*TopK*类中的三个方法:
`TopK(k)`, 构造方法
`add(word)`, 增加一个新单词
`topk()`, 得到当前最常使用的k个单词.
 ### 样例说明
 **样例 1:**
```
输入：
TopK(2)
add("lint")
add("code")
add("code")
topk()
输出：["code", "lint"]
解释：
"code" 出现两次并且 "lint" 出现一次， 它们是出现最频繁的两个单词。
```

**样例 2:**
```
输入：
TopK(1)
add("aa")
add("ab")
topk()
输出：["aa"]
解释：
"aa" 和 "ab" 出现 , 但是aa的字典序小于ab。
```
 ### 参考代码
 考点：
* set和map维护

题解：
查询前k大，考虑使用k大小的set维护即可，map存储每个单词出现的次数，然后重写compare排序方法，在set中自动排序维护，当set大小超出k后，删除最后即可。
```java
import java.util.NavigableSet;

public class TopK {
    private Map<String, Integer> words = null;
    private NavigableSet<String> topk = null;
    private int k;

    private Comparator<String> myComparator = new Comparator<String>() {
        public int compare(String left, String right) {
            if (left.equals(right))
                return 0;

            int left_count = words.get(left);
            int right_count = words.get(right);
            if (left_count != right_count) {
                return right_count - left_count;
            }
            return left.compareTo(right);
        }
    };

    public TopK(int k) {
        // initialize your data structure here
        this.k = k;
        words = new HashMap<String, Integer>();
        topk = new TreeSet<String>(myComparator);
    }

    public void add(String word) {
        // Write your code here
        if (words.containsKey(word)) {
            if (topk.contains(word))
                topk.remove(word);
            words.put(word, words.get(word) + 1);
        } else {
            words.put(word, 1);
        }

        topk.add(word);
        if (topk.size() > k) {
            topk.pollLast();
        }
    }

    public List<String> topk() {
        // Write your code here
        List<String> results = new ArrayList<String>();
        Iterator it = topk.iterator();
        while(it.hasNext()) {
             String str = (String)it.next();
             results.add(str);
        }
        return results;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)