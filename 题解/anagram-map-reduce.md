# 乱序字符串 (Map Reduce版本)
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/anagram-map-reduce/?utm_source=sc-github-wzz)
 ## 题目描述
 用Map来找乱序字符串的列表
 ### 样例说明
 **样例 1:**

```
输入: "lint lint lnit ln"
输出: 
  ["lint", "lint", "lnit"]
  ["ln"]
```

**样例 2:**

```
输入: "ab ba cab"
输出: 
  ["ab", "ba"]
  ["cab"]
```
 ### 参考代码
 ```java
/**
 * Definition of OutputCollector:
 * class OutputCollector<K, V> {
 *     public void collect(K key, V value);
 *         // Adds a key/value pair to the output buffer
 * }
 */
public class Anagram {

    public static class Map {
        public void map(String key, String value, OutputCollector<String, String> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, String value);
            StringTokenizer tokenizer = new StringTokenizer(value);
            while (tokenizer.hasMoreTokens()) {
                String word = tokenizer.nextToken();
                String original = word;
                char[] chars = original.toCharArray();
                Arrays.sort(chars);
                String sorted = new String(chars);
                output.collect(sorted, word);
            }
        }
    }

    public static class Reduce {
        public void reduce(String key, Iterator<String> values, OutputCollector<String, List<String>> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, List<String> value);
            List<String> results = new ArrayList<String>();
            while (values.hasNext()) {
                results.add(values.next());
            }
            output.collect(key, results);
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)