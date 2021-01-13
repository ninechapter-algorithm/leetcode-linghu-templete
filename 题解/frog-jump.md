# 青蛙跳
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/frog-jump/?utm_source=sc-github-wzz)
 ## 题目描述
 一只青蛙正要过河，这条河分成了 x 个单位，每个单位可能存在石头，青蛙可以跳到石头上，但它不能跳进水里。
按照顺序给出石头所在的位置，判断青蛙能否到达最后一块石头所在的位置。刚开始时青蛙在第一块石头上，假设青蛙第一次跳只能跳一个单位的长度。
如果青蛙最后一个跳 k 个单位，那么它下一次只能跳 `k - 1` ，`k` 或者 `k + 1` 个单位。注意青蛙只能向前跳。
 ### 样例说明
 **样例 1:**
```
给出石头的位置为 [0,1,3,5,6,8,12,17]
输入:
[0,1,3,5,6,8,12,17]
输出:
true

解释:
总共8块石头。
第一块石头在 0 位置，第二块石头在 1 位置，第三块石头在 3 位置等等......
最后一块石头在 17 位置。
返回 true。青蛙可以通过跳 1 格到第二块石头，跳 2 格到第三块石头，跳 2 格到第四块石头，跳 3 格到第六块石头，跳 4 格到第七块石头，最后跳 5 格到第八块石头。
```

**样例 2:**
```
给出石头的位置为 `[0,1,2,3,4,8,9,11]`
输入:
[0,1,2,3,4,8,9,11]
输出:
false

解释:
返回 false。青蛙没有办法跳到最后一块石头因为第五块石头跟第六块石头的距离太大了。
```
 ### 参考代码
 dp[stone]为set，记录青蛙可以跳的距离。
状态转移方程为：
跳k - 1到stone + k - 1:dp[stone + k - 1].add(k - 1)
跳k到stone + k:dp[stone + k].add(k)
跳k + 1到stone + k + 1:dp[stone + k + 1].add(k + 1)
```java
public class Solution {
    /**
     * @param stones a list of stones' positions in sorted ascending order
     * @return true if the frog is able to cross the river or false
     */
    public boolean canCross(int[] stones) {
        // Write your code here
        HashMap<Integer, HashSet<Integer>> dp =
            new HashMap<Integer, HashSet<Integer>>(stones.length);
        for (int i = 0; i < stones.length; i++) {
        	dp.put(stones[i], new HashSet<Integer>() );
        }
        dp.get(0).add(0);

        for (int i = 0; i < stones.length - 1; ++i) {
        	int stone = stones[i];
        	for (int k : dp.get(stone)) {
                // k - 1
                if (k - 1 > 0 && dp.containsKey(stone + k - 1))
                    dp.get(stone + k - 1).add(k - 1);
                // k
                if (dp.containsKey(stone + k))
                    dp.get(stone + k).add(k);
                // k + 1
                if (dp.containsKey(stone + k + 1))
                    dp.get(stone + k + 1).add(k + 1);
        	}
        }
        
        return !dp.get(stones[stones.length - 1]).isEmpty();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)