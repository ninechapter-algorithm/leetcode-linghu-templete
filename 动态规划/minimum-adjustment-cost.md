# 最小调整代价
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-adjustment-cost/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给一个整数数组，调整每个数的大小，使得相邻的两个数的差不大于一个给定的整数target，调整每个数的代价为调整前后的差的绝对值，求调整代价之和最小是多少。</p>
 ### 样例说明
 ```
样例 1:
	输入:  [1,4,2,3], target=1
  输出:  2

样例 2:
	输入:  [3,5,4,7], target=2
	输出:  1
	
```
 ### 参考代码
 f[i][k] 表示第i个数变成k时，前i个数调整的代价和最小值。
枚举第i-1个数调整成的数字j，再枚举第i个数调整成k.做转移。
```
[[python]]
class Solution:
    # @param A: An integer array.
    # @param target: An integer.
    def MinAdjustmentCost(self, A, target):
        # write your code here
        f = [[ sys.maxint for j in xrange(101)] for i in xrange(len(A)+1)]
        for i in xrange(101):
            f[0][i] = 0
        n = len(A)
        for i in xrange(1,n+1):
            for j in xrange(101):
                if f[i-1][j] != sys.maxint:
                    for k in xrange(101):
                        if abs(j-k) <= target:
                            f[i][k] = min(f[i][k], f[i-1][j] + abs(A[i-1]-k))
        ans = f[n][100]
        for i in xrange(101):
            if f[n][i] < ans:
                ans = f[n][i]       

        return ans
[[java]]
public class Solution {
    /**
     * @param A: An integer array.
     * @param target: An integer.
     */
    public int MinAdjustmentCost(ArrayList<Integer> A, int target) {
        // write your code here
        int n = A.size();
        int[][] f = new int[n + 1][101];
        for (int i = 0; i <= n ; ++i)
            for (int j = 0; j <=100; ++j)
                f[i][j] = Integer.MAX_VALUE;
        for (int i = 0; i <= 100; ++i)
            f[0][i] = 0;
        for (int i = 1; i <=n; ++i)
            for (int  j = 0; j <= 100;++j)
                if (f[i-1][j] != Integer.MAX_VALUE)
                for (int k = 0; k <= 100; ++k)
                    if (Math.abs(j-k) <= target)
                    if (f[i][k] > f[i-1][j] + Math.abs(A.get(i-1)-k))
                        f[i][k] = f[i-1][j] + Math.abs(A.get(i-1)-k);  
        int ans = Integer.MAX_VALUE;
        for (int i = 0; i <= 100; ++i)
            if (f[n][i] < ans)
                ans = f[n][i];
        return ans; 
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)