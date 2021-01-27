# 迷你Cassandra
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/mini-cassandra/?utm_source=sc-github-wzz)
 ## 题目描述
 Cassandra是一个NoSQL数据库。Cassandra中的一个单独数据条目由3部分构成：

1. row_key (相当于于哈希值)
2. column_key
3. value

row_key 用于哈希，不支持范围查询。我们将其简化为字符串。
column_key 已排序并支持范围查询。我们将其简化为整数。
value 是一个字符串。你可以将任何数据序列化为字符串并将其存储在值中。

现在要实现下面两个方法：

1. `insert(row_key, column_key, value)`
2. `query(row_key, column_start, column_end)`  返回条目列表
 ### 样例说明
 **样例 1:**

```
输入:
  insert("google", 1, "haha")
  query("google", 0, 1)
输出: [(1, "haha")]
```

**样例 2:**

```
输入: 
  insert("google", 1, "haha")
  insert("lintcode", 1, "Good")
  insert("google", 2, "hehe")
  query("google", 0, 1)
  query("google", 0, 2)
  query("go", 0, 1)
  query("lintcode", 0, 10)
输出: 
  [(1, "haha")]
  [(1, "haha"),(2, "hehe")]
  []
  [(1, "Good")]
```
 ### 参考代码
 注意: 一个 row_key 可以对应多个 Column; 而一个 row_key 和一个 column_key 是唯一确定对应的 value 的.

可以使用哈希表套哈希表实现: `map<row_key, map<column_key, value>>` 

每次 `insert` 直接更新 value 即可.

而 `query` 则需要取出一个 row_key 对应的所有的 <column_key, value> 对, 如果 column_key 在给定范围内时, 放入答案序列中即可.
```java
/**
 * Definition of Column:
 * public class Column {
 *     public int key;
 *     public String value;
 *     public Column(int key, String value) {
 *         this.key = key;
 *         this.value = value;
 *    }
 * }
 */
public class MiniCassandra {

    private Map<String, NavigableMap<Integer, String>> hash;

    public MiniCassandra() {
        // initialize your data structure here.
        hash = new HashMap<String, NavigableMap<Integer, String>>();
    }

    /**
     * @param raw_key      a string
     * @param column_start an integer
     * @param column_end   an integer
     * @return void
     */
    public void insert(String raw_key, int column_key, String column_value) {
        // Write your code here
        if (!hash.containsKey(raw_key))
            hash.put(raw_key, new TreeMap<Integer, String>());
        hash.get(raw_key).put(column_key, column_value);
    }

    /**
     * @param raw_key      a string
     * @param column_start an integer
     * @param column_end   an integer
     * @return a list of Columns
     */
    public List<Column> query(String raw_key, int column_start, int column_end) {
        // Write your code here
        List<Column> rt = new ArrayList<Column>();
        if (!hash.containsKey(raw_key))
            return rt;
        for (Map.Entry<Integer, String> entry : hash.get(raw_key).subMap(column_start, true, column_end, true)
                .entrySet()) {
            rt.add(new Column(entry.getKey(), entry.getValue()));
        }
        return rt;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)