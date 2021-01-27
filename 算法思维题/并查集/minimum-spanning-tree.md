# 最小生成树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-spanning-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一些Connections，即Connections类，找到一些能够将所有城市都连接起来并且花费最小的边。
如果说可以将所有城市都连接起来，则返回这个连接方法；不然的话返回一个空列表。
 ### 样例说明
 **样例 1:**
```
输入:
["Acity","Bcity",1]
["Acity","Ccity",2]
["Bcity","Ccity",3]
输出:
["Acity","Bcity",1]
["Acity","Ccity",2]
```

**样例 2:**
```
输入:
["Acity","Bcity",2]
["Bcity","Dcity",5]
["Acity","Dcity",4]
["Ccity","Ecity",1]
输出:
[]

解释:
没有办法连通
```
 ### 参考代码
 用map存储自动排序，再利用并查集，连通的点根应该相同。
```cpp
/**
 * Definition for a Connection.
 * class Connection {
 * public:
 *   string city1, city2;
 *   int cost;
 *   Connection(string& city1, string& city2, int cost) {
 *       this->city1 = city1;
 *       this->city2 = city2;
 *       this->cost = cost;
 * }
 */
bool cmp(const Connection& c1, const Connection& c2) {
    if (c1.cost != c2.cost)
        return c1.cost < c2.cost;

    if (c1.city1 != c2.city1)
        return c1.city1 < c2.city1;

    return c1.city2 < c2.city2;
}

class Solution {
public:
    /**
     * @param connections given a list of connections include two cities and cost
     * @return a list of connections from results
     */
    vector<Connection> lowestCost(vector<Connection>& connections) {
        // Write your code here
        sort(connections.begin(), connections.end(), cmp);
        unordered_map<string, int> hash;
        int n = 0;
        for (auto connection : connections) {
            if (hash.find(connection.city1) == hash.end()) {
                hash[connection.city1] = ++n;
            }
            if (hash.find(connection.city2) == hash.end()) {
                hash[connection.city2] = ++n;
            }
        }

        vector<int> father(n + 1, 0);

        vector<Connection> results;
        for (auto connection : connections) {
            int num1 = hash[connection.city1];
            int num2 = hash[connection.city2];

            int root1 = find(num1, father);
            int root2 = find(num2, father);
            if (root1 != root2) {
                father[root1] = root2;
                results.push_back(connection);
            }
        }

        if (results.size() != n - 1)
            return vector<Connection>();
        return results;
    }

    int find(int num, vector<int>& father) {
        if (father[num] == 0)
            return num;

        return father[num] = find(father[num], father);
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)