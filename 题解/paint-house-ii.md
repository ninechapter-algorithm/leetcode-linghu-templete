# 房屋染色 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/paint-house-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 这里有`n`个房子在一列直线上，现在我们需要给房屋染色，共有`k`种颜色。每个房屋染不同的颜色费用也不同，你需要设计一种染色方案使得相邻的房屋颜色不同，并且费用最小。

费用通过一个`n`x`k` 的矩阵给出，比如`cost[0][0]`表示房屋`0`染颜色`0`的费用，`cost[1][2]`表示房屋`1`染颜色`2`的费用。
 ### 样例说明
 **样例1**

```plain
输入:
costs = [[14,2,11],[11,14,5],[14,3,10]]
输出: 10
说明:
三个屋子分别使用第1,2,1种颜色，总花费是10。
```

**样例2**

```plain
输入:
costs = [[5]]
输出: 5
说明：
只有一种颜色，一个房子，花费为5
```


 ### 参考代码
 ```cpp
class node {
public: 
    node(){}
    node(int x, int v) {
        id = x;
        value = v;
    }
    int id, value;
};

bool cmp(const node &a, const node &b)  {
    return a.value < b.value;
}

class Solution {
public:
    
    int minCostII(vector<vector<int>>& costs) {
        if(costs.size() == 0) {
            return 0;
        }
        int n = costs.size();
        int k = costs[0].size();
        int ans[n+1][k];
        memset(ans, 0, sizeof(ans));
        vector<node> now(3), last(3);
        now[0] = node(0, INT_MAX);
        now[1] = node(0, INT_MAX);
            
        for (int i = 1; i <= n; i++) {
            last = now;
            now[0] = node(0, INT_MAX);
            now[1] = node(0, INT_MAX);
            for (int j = 0; j < k ; j++) {
                if(j == last[0].id) {
                    ans[i][j] = ans[i-1][last[1].id] + costs[i-1][j]; 
                } else {
                    ans[i][j] = ans[i-1][last[0].id] + costs[i-1][j];
                }
                now[2] = node(j, ans[i][j]);
                sort(now.begin(), now.end(), cmp);
            }
        }
        
        return now[0].value;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)