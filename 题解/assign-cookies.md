# 分饼干
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/assign-cookies/?utm_source=sc-github-wzz)
 ## 题目描述
 假设你是一个了不起的家长，准备给你的孩子们一些饼干吃，但是你只能给每个孩子至多一块饼干。每一块饼干$j$都有一个尺寸$s_{j}$；同时每一个孩子$i$都有一个贪吃指数$g_{i}$，代表了能使他满足的最小的饼干尺寸。如果$s_{j} \geq g_{i}$，那么就可以将饼干$j$分给孩子$i$使他得到满足。你的目标是使最多的孩子得到满足，输出这个最大值。
 ### 样例说明
 **样例1：**

```
输入：[1,2,3], [1,1]
输出：1
说明：你有三个孩子和两块饼干，三个孩子的贪吃指数分别是1，2，3
虽然你有两块饼干，但是因为它们的大小都为1，你只能满足让贪吃指数为1的孩子满足，因此你应该输出1
```

**样例2：**

```
输入：[1,2], [1,2,3]
输出：2
说明：你有两个孩子和三块饼干，两个孩子的贪吃指数分别是1和2
这三块饼干的大小足以满足所有的孩子，因此你应该输出2
```
 ### 参考代码
 <p><blockquote style="margin: 0 0 0 40px; border: none; padding: 0px;"><p><br></p></blockquote></p>
```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(s.begin(), s.end());
        sort(g.begin(), g.end());
        int i, j;
        for (i = j = 0; i < g.size() && j < s.size(); j++) {
            if (g[i] <= s[j]) {
                i++;
            }
        }
        return i;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)