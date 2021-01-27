# 字符计数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/count-characters/?utm_source=sc-github-wzz)
 ## 题目描述
 对一个字符串中的字符进行计数, 返回一个hashmap, key为字符, value是这个字符出现的次数.
 ### 样例说明
 
例1:
```
输入:
str = "abca"

输出:
{
  "a": 2,
  "b": 1,
  "c": 1
}

```
例2:
```
输入:
str = "ab"

输出:
{
  "a": 1,
  "b": 1
}

```

 ### 参考代码
 利用map统计即可
```java
public class Solution {
    /*
     * @param : a string
     * @return: a hash map
     */
    public Map<Character, Integer> countCharacters(String str) {
        // Write your code here
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        for (char c : str.toCharArray()) {
            if (!map.containsKey(c)) {
                map.put(c, 1);
            } else {
                map.put(c, map.get(c) + 1);
            }
        }
        return map;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)