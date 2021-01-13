# 更新二进制位
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/update-bits/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出两个32位的整数N和M，以及两个二进制位的位置i和j。写一个方法来使得N中的第i到j位等于M（M会是N中从第i为开始到第j位的子串）</p>
 ### 样例说明
 **样例1:**
```
输入: N=(10000000000)2 M=(10101)2 i=2 j=6
输出: N=(10001010100)2
```


**样例 2:**
```
输入: N=(10000000000)2 M=(11111)2 i=2 j=6
输出: N=(10001111100)2
```

 ### 参考代码
 ```java
class Solution {
    /**
     *@param n, m: Two integer
     *@param i, j: Two bit positions
     *return: An integer
     */
    public int updateBits(int n, int m, int i, int j) {
        // write your code here
        int max = ~0; /* All 1’s */
        // 1’s through position j, then 0’s
        if (j == 31)
            j = max;
        else
            j = (1 << (j + 1)) - 1;
        int left = max - j;
        // 1’s after position i
	    int right = ((1 << i) - 1);
	    // 1’s, with 0s between i and j
        int mask = left | right;
        // Clear i through j, then put m in there
        return ((n & mask) | (m << i));
    }
}


```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)