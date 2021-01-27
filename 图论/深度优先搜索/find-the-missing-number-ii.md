# 寻找丢失的数 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-the-missing-number-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个由 1 - `n` 的整数随机组成的一个字符串序列，其中丢失了一个整数，请找到它。
 ### 样例说明
 **样例1**

```
输入: n = 20 和 str = 19201234567891011121314151618
输出: 17
解释:
19'20'1'2'3'4'5'6'7'8'9'10'11'12'13'14'15'16'18
```

**样例2**

```
输入: n = 6 和 str = 56412
输出: 3
解释:
5'6'4'1'2
```
 ### 参考代码
 dfs求解，首先考虑搜索大的数字，这样搜索速度能快一些
```java
public class Solution {
    /**
     * @param n an integer
     * @param str a string with number from 1-n
     *            in random order and miss one number
     * @return an integer
     */   
    public boolean flag = false;
    public int ans = 0;
    public int findMissing2(int n, String str) {
        boolean[] happen = new boolean[n + 1];
        dfs(0, n, str, happen);
        return ans;
    }
    
    public void dfs(int i, int n, String s, boolean[] happen) {
        if (i >= s.length() || flag) {
        	if (!flag)
            for (int k = 1; k <= n; k++) {
                if (!happen[k]) {
                    ans = k;
                }
            }
        	flag = true;
            return;
        }
        int sum = s.charAt(i) - '0';
        int j = i;
        if (sum == 0) {
            return;
        }
        while (sum <= n) {
            if (!happen[sum]) {
                happen[sum] = true;
                dfs(j+1, n, s, happen);
                happen[sum] = false;
            }
            j++;
            if (j >= s.length()) {
                break;
            }
            sum = sum * 10 + (s.charAt(j) - '0');
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)