# 重新安排行程
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/reconstruct-itinerary/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个机票的字符串二维数组 [from, to]，子数组中的两个成员分别表示飞机出发和降落的机场地点，对该行程进行重新规划排序。所有这些机票都属于一个从JFK（肯尼迪国际机场）出发的先生，所以该行程必须从 JFK 出发。
 ### 样例说明
 **示例1**
```
输入： [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
输出： ["JFK", "MUC", "LHR", "SFO", "SJC"].
```
**示例2**
```
输入：[["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
输出：["JFK","ATL","JFK","SFO","ATL","SFO"].
解释：另一种有效的行程是 ["JFK","SFO","ATL","JFK","ATL","SFO"]。但是它自然排序更大更靠后。
```
 ### 参考代码
 使用优先队列存储从一个机场出发可以到达的所有机场，再进行DFS找出答案
```java
public class Solution {
    public List<String> findItinerary(String[][] tickets) {
        Map<String, PriorityQueue<String>> hashmap = new HashMap<String, PriorityQueue<String>>();
        List<String> list = new ArrayList<String>();
        String cur = "JFK";
        int length = tickets.length;
        for (int i = 0; i < length; i++) {
            if (!hashmap.containsKey(tickets[i][0])) {
                hashmap.put(tickets[i][0], new PriorityQueue<String>());
            }
            hashmap.get(tickets[i][0]).add(tickets[i][1]);
        }
        dfs(cur, hashmap, list);
        Collections.reverse(list);
        return list;
    }
    public void dfs(String cur, Map<String, PriorityQueue<String>> hashmap, List<String> list) {
        while (hashmap.containsKey(cur) && !hashmap.get(cur).isEmpty()) {
            dfs(hashmap.get(cur).poll(), hashmap, list);
        }
        list.add(cur);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)