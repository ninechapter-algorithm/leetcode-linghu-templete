# H指数 II





 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/h-index-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一位研究者论文被引用次数的数组（被引用次数是非负整数），数组已经按照升序排列。编写一个方法，计算出研究者的 h 指数。

h 指数的定义: “h 代表“高引用次数”（high citations），一名科研人员的 h 指数是指他（她）的 （N 篇论文中）至多有 h 篇论文分别被引用了至少 h 次。（其余的 N - h 篇论文每篇被引用次数不多于 h 次。）"

 ### 样例说明
 ```
输入: citations = [0,1,3,5,6]
输出: 3 
解释: 给定数组表示研究者总共有 5 篇论文，每篇论文相应的被引用了 0, 1, 3, 5, 6 次。
     由于研究者有 3 篇论文每篇至少被引用了 3 次，其余两篇论文每篇被引用不多于 3 次，所以她的 h 指数是 3。
```
 ### 参考代码
 ```cpp
class Solution {
public:
    int hIndex(vector<int>& citations) {
        int ans = 0;
        int h;
        int l = 0, r = citations.size() - 1;
        
        while(l <= r) {
            int mid = (l + r)/2;
            h = citations.size() - mid;
            if (citations[mid] >= h) {
                ans = max(ans, h);
                r = mid - 1;
            } else {
                ans = max(ans, citations[mid]);
                l = mid + 1;
            }
        }
        return ans;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)