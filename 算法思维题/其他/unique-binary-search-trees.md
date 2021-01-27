# 不同的二叉查找树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/unique-binary-search-trees/?utm_source=sc-github-wzz)
 ## 题目描述
 给出 *n*，问由 1...*n* 为节点组成的不同的二叉查找树有多少种？
 ### 样例说明
 **样例 1：**
```
输入：n = 3
输出：5
解释：有5种不同形态的二叉查找树：
```

	1           3    3       2      1
	 \         /    /       / \      \
	  3      2     1       1   3      2
	 /      /       \                  \
	2     1          2                  3
 ### 参考代码
 Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

For example,
Given n = 3, there are a total of 5 unique BST's.

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```java
public class Solution {
/*
The case for 3 elements example
Count[3] = Count[0]*Count[2]  (1 as root)
              + Count[1]*Count[1]  (2 as root)
              + Count[2]*Count[0]  (3 as root)

Therefore, we can get the equation:
Count[i] = ∑ Count[0...k] * [ k+1....i]     0<=k<i-1  

*/
    public int numTrees(int n) {
        int[] count = new int[n + 2];
        count[0] = 1;
        count[1] = 1;
        
        for(int i = 2; i <= n; i++){
            for(int j = 0; j < i; j++){
                count[i] += count[j] * count[i - j - 1];
            }
        }
        return count[n];
    }
}


```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)