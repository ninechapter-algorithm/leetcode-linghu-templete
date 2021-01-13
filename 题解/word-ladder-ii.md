# 单词接龙 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/word-ladder-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给出两个单词（*start*和*end*）和一个字典，找出所有从*start*到*end*的最短转换序列。

变换规则如下：

1. 每次只能改变一个字母。
2. 变换过程中的中间单词必须在字典中出现。

 ### 样例说明
 **样例 1:**
```
输入：start = "a"，end = "c"，dict =["a","b","c"]
输出：[["a","c"]]
解释：
"a"->"c"
```

**样例 2:**
```
输入：start ="hit"，end = "cog"，dict =["hot","dot","dog","lot","log"]
输出：[["hit","hot","dot","dog","cog"],["hit","hot","lot","log","cog"]]
解释：
1."hit"->"hot"->"dot"->"dog"->"cog"
2."hit"->"hot"->"lot"->"log"->"cog"
第一个序列的字典序小于第二个。
```
 ### 参考代码
 end -> start : bfs
start -> end : dfs
```java
public class Solution {
    public List<List<String>> findLadders(String start, String end,
            Set<String> dict) {
        List<List<String>> ladders = new ArrayList<List<String>>();
        Map<String, List<String>> map = new HashMap<String, List<String>>();
        Map<String, Integer> distance = new HashMap<String, Integer>();

        dict.add(start);
        dict.add(end);
 
        bfs(map, distance, end, start, dict);
        
        List<String> path = new ArrayList<String>();
        
        dfs(ladders, path, start, end, distance, map);

        return ladders;
    }

    void dfs(List<List<String>> ladders, List<String> path, String crt,
            String end, Map<String, Integer> distance,
            Map<String, List<String>> map) {
        path.add(crt);
        if (crt.equals(end)) {
            ladders.add(new ArrayList<String>(path));
        } else {
            for (String next : map.get(crt)) {
                if (distance.containsKey(next) && distance.get(crt) == distance.get(next) + 1) { 
                    dfs(ladders, path, next, end, distance, map);
                }
            }           
        }
        path.remove(path.size() - 1);
    }

    void bfs(Map<String, List<String>> map, Map<String, Integer> distance,
            String start, String end, Set<String> dict) {
        Queue<String> q = new LinkedList<String>();
        q.offer(start);
        distance.put(start, 0);
        for (String s : dict) {
            map.put(s, new ArrayList<String>());
        }
        
        while (!q.isEmpty()) {
            String crt = q.poll();

            List<String> nextList = expand(crt, dict);
            for (String next : nextList) {
                map.get(next).add(crt);
                if (!distance.containsKey(next)) {
                    distance.put(next, distance.get(crt) + 1);
                    q.offer(next);
                }
            }
        }
    }

    List<String> expand(String crt, Set<String> dict) {
        List<String> expansion = new ArrayList<String>();

        for (int i = 0; i < crt.length(); i++) {
            for (char ch = 'a'; ch <= 'z'; ch++) {
                if (ch != crt.charAt(i)) {
                    String expanded = crt.substring(0, i) + ch
                            + crt.substring(i + 1);
                    if (dict.contains(expanded)) {
                        expansion.add(expanded);
                    }
                }
            }
        }

        return expansion;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)