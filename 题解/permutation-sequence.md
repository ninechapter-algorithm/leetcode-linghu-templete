# 第k个排列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/permutation-sequence/?utm_source=sc-github-wzz)
 ## 题目描述
 给定 *n* 和 *k*，求n的全排列中字典序第k个排列.
 ### 样例说明
 **样例 1:**

```
输入: n = 3, k = 4
输出: "231"
解释: 
n = 3时, 全排列如下:
"123", "132", "213", "231", "312", "321"
```

**样例 2:**

```
输入: n = 1, k = 1
输出: "1"
```
 ### 参考代码
 康拓展开的应用, 模板题.

康拓展开, 计算排列与字典序排名的映射关系.

[维基百科 康拓展开](https://zh.wikipedia.org/wiki/%E5%BA%B7%E6%89%98%E5%B1%95%E5%BC%80)
```java
public class Solution {

    public String getPermutation(int n, int k) {
        StringBuilder sb = new StringBuilder();
        boolean[] used = new boolean[n];

        k = k - 1;
        int factor = 1;
        for (int i = 1; i < n; i++) {
            factor *= i;
        }

        for (int i = 0; i < n; i++) {
            int index = k / factor;
            k = k % factor;
            for (int j = 0; j < n; j++) {
                if (used[j] == false) {
                    if (index == 0) {
                        used[j] = true;
                        sb.append((char) ('0' + j + 1));
                        break;
                    } else {
                        index--;
                    }
                }
            }
            if (i < n - 1) {
                factor = factor / (n - 1 - i);
            }
        }

        return sb.toString();
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)