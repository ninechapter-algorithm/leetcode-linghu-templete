# 丢鸡蛋
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/drop-eggs/?utm_source=sc-github-wzz)
 ## 题目描述
 楼有 `n` 层高，鸡蛋若从 *k* 层或以上扔，就会碎。从 *k* 层以下扔，就不会碎。

现在给两个鸡蛋，用最少的扔的次数找到 *k*。返回最坏情况下次数。
 ### 样例说明
 **样例 1：**
```
输入：100
输出：14
```
**样例 2：**
```
输入：10
输出：4
```
 ### 参考代码
 ```cpp
class Solution {
public:
    /**
     * @param n an integer
     * @return an integer
     */
    int dropEggs(int n) {
        // Write your code here
        long long ans = 0;
        int x = 0;
        while (ans < n) {
            x += 1;
            ans += x;
        }
        return x;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)