# N-Gram (Map Reduce)
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/n-gram-map-reduce/?utm_source=sc-github-wzz)
 ## 题目描述
 给出若干字符串和数字 N。用 Map Reduce 的方法统计所有 N-Grams 及其出现次数 。以字母为粒度。
 ### 样例说明
 
 ### 参考代码
 遍历每个字符串，从每个位置开始，截取一定长度的子串，记录即可
```java
/**
 * Definition of OutputCollector:
 * class OutputCollector<K, V> {
 *     public void collect(K key, V value);
 *         // Adds a key/value pair to the output buffer
 * }
 */
public class NGram {

    public static class Map {
        public void map(String _, int n, String str,
                        OutputCollector<String, Integer> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, Integer value);
            for (int index = 0; index < str.length() - n + 1; ++index) {
                output.collect(str.substring(index, index + n), 1);
            }
        }
    }

    public static class Reduce {
        public void reduce(String key, Iterator<Integer> values,
                           OutputCollector<String, Integer> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, int value);
            int sum = 0;
            while (values.hasNext()) {
                    sum += values.next();
            }
            output.collect(key, sum);
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)