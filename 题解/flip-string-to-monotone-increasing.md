# 将字符串翻转到单调递增
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/flip-string-to-monotone-increasing/?utm_source=sc-github-wzz)
 ## 题目描述
 如果一个由 `'0'` 和 `'1'` 组成的字符串，是以一些 `'0'`（可能没有 `'0'`）后面跟着一些 `'1'`（也可能没有 `'1'`）的形式组成的，那么该字符串是*单调递增*的。

我们给出一个由字符 `'0'` 和 `'1'` 组成的字符串 `S`，我们可以将任何 `'0'` 翻转为 `'1'` 或者将 `'1'` 翻转为 `'0'`。

返回使 `S` 单调递增的最小翻转次数。
 ### 样例说明
 **样例 1:**
```
输入："00110"
输出：1
解释：
我们翻转最后一位得到 00111.
```
**样例 2:**
```
输入："010110"
输出：2
解释：
我们翻转得到 011111，或者是 000111。
```
 ### 参考代码
 枚举法（Enumeration）
使用 PrefixSum 记录某个位置及往左的位置上有多少个 1。
循环每个位置，计算左侧变为 0，右侧变为 1 的耗费，记录下所有的耗费中的最小耗费。
```java
class Solution {
    public int minFlipsMonoIncr(String S) {
        int[] leftOnes = new int[S.length()];
        int ones = 0;
        for (int i = 0; i < S.length(); i++) {
            if (S.charAt(i) == '1') {
                ones++;
            }
            leftOnes[i] = ones;
        }
        
        int flips = S.length() - ones;
        for (int i = 0; i < S.length(); i++) {
            int rightOnes = ones - leftOnes[i];
            int rightZeroes = S.length() - i - 1 - rightOnes;
            flips = Math.min(flips, leftOnes[i] + rightZeroes);
        }
                             
        return flips;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)