# 不包括连续1的非负整数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/non-negative-integers-without-consecutive-ones/?utm_source=sc-github-wzz)
 ## 题目描述
 给定正整数n，找到小于或等于n的**非负**整数的个数，要求它们的二进制表示不包含**连续的1**。
 ### 样例说明
 **样例 1:**
```
输入：5
输出：5
解释：
以下是非负整数<= 5及其对应的二进制表示：
0：0
1：1
2：10
3：11
4：100
5：101
其中，只有整数3违反规则（两个连续的1），另外5个满足规则。
```



**样例 2:**
```
输入：6
输出：5
解释：
以下是非负整数<= 6及其对应的二进制表示：
0 : 0
1 : 1
2 : 10
3 : 11
4 : 100
5 : 101
6 : 110
其中，只有整数3和6违反规则（两个连续的1），另外5个满足规则。
```
 ### 参考代码
 考点：
* dp

题解：
* 数字n转化为01字符串,从前向后遍历，f[i]表示当前i为'1'时，i位其右侧01串排列的合法方案。
* f[i] = f[i - 1] + f[i - 2]，此处求出i位的右侧的01串排列的合法方案，可以由i - 1时尾部加上一个'0'转移到i，可以由i - 2时尾部加上'01'转移到i。
* 从高位向低位遍历，每次遇到为'1'的位时，加上f[i]即可，遇到连续两个'1'时，返回即可。
```java
public class Solution {
    public int findIntegers(int num) {
        if (num < 2) {
            return num + 1;
        }
        
        StringBuilder str = new StringBuilder(Integer.toBinaryString(num)).reverse();
        int k = str.length();
        
        int[] f = new int[k];
        f[0] = 1;
        f[1] = 2;
        for (int i = 2; i < k; i++) {   //f[i]表示当前i为'1'时，i位其右侧01串排列的合法方案。
            f[i] = f[i - 1] + f[i - 2];	//f[i] = f[i - 1] + f[i - 2]，此处求出i位的右侧的01串排列的合法方案，可以由i - 1时尾部加上一个'0'转移到i，可以由i - 2时尾部加上'01'转移到i。
        }
        
        int ans = 0;
        for (int i = k - 1; i >= 0; i--) {
            if (str.charAt(i) == '1') {
                ans += f[i];			//每次遇到为'1'的位时，加上f[i]即可
                if (i < k - 1 && str.charAt(i + 1) == '1') {
                    return ans;
                }
            }
        }
        ans++;		//加上自身数字
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)