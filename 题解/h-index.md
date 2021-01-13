# H指数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/h-index/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个研究员的引用量数组（每个引用量都是一个非负整数）。请计算该研究员的H指数。

一个研究者的H指数为h，意味着他的论文中，有h篇有至少有h个引用量。
 ### 样例说明
 **样例1**

```
输入: citations = [3, 0, 6, 1, 5]
输出: 3
解释:
研究者有5篇论文，每一篇的引用量为3，0，6，1，5。因为研究者有三篇论文至少有3个引用，而剩下两篇则引用不足3次，所以他的H指数为3
```

**样例2**

```
输入: citations = [5, 5, 5, 5, 5]
输出: 5
解释:
研究者有5篇论文，每一篇的引用量为5, 5, 5, 5, 5。因为研究者有5篇论文至少有5个引用，所以他的H指数为5
```

 ### 参考代码
 求出一个后缀和数组，这个数组下标i对应的数表示大于等于i的数字出现的次数，这个数组可以O(n)求出
然后从大到小枚举这些数，找到最大的满足条件的数即可
总复杂度O(n)
```cpp
class Solution {
public:
    int hIndex(vector<int>& citations) {
        int n = citations.size();
        int num[n+1];
        memset(num, 0, sizeof(num));
        
        for (int i = 0; i < citations.size(); i++) {
            if (citations[i] >= n) {
                num[n] ++;
            } else {
                num[citations[i]] ++;
            }
        }
        int sum = 0;
        for (int i = n; i >= 0; i--) {
            sum += num[i];
            if(sum >= i)
                return i;
        }
        return 0;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)