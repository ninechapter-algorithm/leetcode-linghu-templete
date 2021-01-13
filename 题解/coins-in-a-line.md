# 硬币排成线
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/coins-in-a-line/?utm_source=sc-github-wzz)
 ## 题目描述
 有 `n` 个硬币排成一条线。两个参赛者轮流从右边依次拿走 1 或 2 个硬币，直到没有硬币为止。拿到最后一枚硬币的人获胜。

请判定 **先手玩家** 必胜还是必败?

若必胜, 返回 `true`, 否则返回 `false`.
 ### 样例说明
 **样例 1:**

```
输入: 1
输出: true
```

**样例 2:**

```
输入: 4
输出: true
解释: 
先手玩家第一轮拿走一个硬币, 此时还剩三个.
这时无论后手玩家拿一个还是两个, 下一次先手玩家都可以把剩下的硬币拿完.
```
 ### 参考代码
 可以证明, 当硬币数目是3的倍数的时候, 先手玩家必败, 否则他必胜.

当硬币数目是3的倍数时, 每一轮先手者拿a个, 后手者拿3-a个即可, 后手必胜.

若不是3的倍数, 先手者可以拿1或2个, 此时剩余硬币个数就变成了3的倍数.
```cpp
class Solution {
public:
    /**
     * @param n: An integer
     * @return: A boolean which equals to true if the first player will win
     */
    bool firstWillWin(int n) {
        return n % 3;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)