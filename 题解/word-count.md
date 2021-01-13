# 单词计数 (Map Reduce版本)
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/word-count/?utm_source=sc-github-wzz)
 ## 题目描述
 使用 map reduce 来计算单词频率
https://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html#Example%3A+WordCount+v1.0

 ### 样例说明
 
 ### 参考代码
 ```java
/**
 * Definition of OutputCollector:
 * class OutputCollector<K, V> {
 *     public void collect(K key, V value);
 *         // Adds a key/value pair to the output buffer
 * }
 */
public class WordCount {

    public static class Map {
        public void map(String key, String value, OutputCollector<String, Integer> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, int value);
            StringTokenizer tokenizer = new StringTokenizer(value);
            while (tokenizer.hasMoreTokens()) {
                String word = tokenizer.nextToken();
                output.collect(word, 1);
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