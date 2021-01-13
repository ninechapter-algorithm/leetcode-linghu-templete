# 我能赢吗
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/can-i-win/?utm_source=sc-github-wzz)
 ## 题目描述
 在 "100 game" 中, 两位玩家交替使用 1 到 10 的任意一个整数加到一个和中, 谁加完之后, 和达到或者超过了 100 就获胜.

如果我们改变规则, 玩家不能重复使用已经使用过的整数呢？

举个例子, 两个玩家可以轮流从一个共同的数字池 (里面的整数为 1 到 15) 中拿出整数, 拿出之后不放回, 直到某个玩家拿出一个数字之后, 已经拿出的数字之和达到或者超过了 100, 该玩家获胜.

给定两个整数 `maxChoosableInteger` 和 `desiredTotal`, 表示刚开始数字池中有 `1, 2, 3, ..., maxChoosableInteger` 这些数字, 获胜的目标和是 `desiredTotal`. 

判断先手玩家是否必胜, 假设两个玩家都用了最佳策略.
 ### 样例说明
 **样例 1:**

```
输入: maxChoosableInteger = 10, desiredTotal = 11
输出: false
解释: 
    无论第一个玩家怎么选都会输. 
    如果他没选 10, 那么第二个玩家选择 10 就可以取得胜利.
    如果他选了 10, 那么第二个玩家可以选择任意一个数取得胜利.
```

**样例 2:**

```
输入: maxChoosableInteger = 10, desiredTotal = 10
输出: true
解释: 第一个玩家直接选择 10 就可以取得胜利.
```
 ### 参考代码
 这是一道状态压缩动态规划问题. (你也可以不压缩, 使用哈希表, 可能会 MLE 或 TLE)

设定 dp[S] 表示还剩下集合S里的数字时, 先手的人是否有必胜策略.

状态转移很容易想出来: 如果集合 S 中存在一个数 i, 使得拿走 i 之后剩下的集合 T 是必败的, 那么集合 S 就是必胜的状态.

边界状态: 对于集合 S, 我们可以知道已经拿出去的数的和, 如果这个和加上集合 S 中最大的元素会达到或超过 desiredTotal, 那么 S 就是必胜的.

推荐使用记忆化搜索来实现.

状态压缩: 用一个整型表示集合S, 即这个整型的第 i 个二进制位为 1 表示集合 S 含有 i.
```java
public class Solution {
    int[] dp;
    boolean[] used;
    public boolean canIWin(int maxChoosableInteger, int desiredTotal) {
        int sum = (1 + maxChoosableInteger) * maxChoosableInteger / 2;
        if (sum < desiredTotal) {       //取完所有数，也达不到desiredTotal，无法赢得游戏
            return false;
        }
        if (desiredTotal <= maxChoosableInteger) {     //第一步就可以获得胜利
            return true;
        }
        dp = new int[1 << maxChoosableInteger];
        Arrays.fill(dp , -1);
        used = new boolean[maxChoosableInteger + 1];

        return helper(desiredTotal);
    }

    public boolean helper(int desiredTotal) {
        if (desiredTotal <= 0) {
            return false;
        }
        int key = format(used);         //把used数组转为十进制表示
        if (dp[key] == -1) {
            for (int i = 1; i < used.length; i++) {  //枚举未选择的数
                if (!used[i]) {
                    used[i] = true;

                    if (!helper(desiredTotal - i)) {
                        dp[key] = 1;
                        used[i] = false;
                        return true;
                    }
                    used[i] = false;
                }
            }
            dp[key] = 0;
        }
        return dp[key] == 1;
    }


    public int format(boolean[] used) {
        int num = 0;
        for (boolean b : used) {
            num <<= 1;
            if (b) {
                num |= 1;
            }
        }
        return num;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)