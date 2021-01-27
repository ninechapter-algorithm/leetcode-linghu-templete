# 邮局问题
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/post-office-problem/?utm_source=sc-github-wzz)
 ## 题目描述
 在一条直线上有 `n` 个房子, 给定数组 `A`, `A[i]` 表示第 `i` 栋房子的位置. 现在需要选择 `k` 个位置建立邮局. 问这 `n` 栋房子到最近邮局的距离总和最小是多少?
 ### 样例说明
 **样例 1:**

```
输入: A = [1, 2, 3, 4, 5], k = 2
输出: 3
解释: 在 2 和 4 建立邮局.
```

**样例 2:**

```
输入: A = [1, 2], k = 1
输出: 1
解释: 在 1 或 2 建立邮局都可以.
```
 ### 参考代码
 线性动态规划 (而不是区间动态规划) 

可以按照每个房子最近的邮局, 把 `n` 个房子分成 `k` 段, 而我们要决定的就是这 `k` 段分别是多长. 为了处理方便我们先对房子的位置排序.

设定 f[i][j] 表示前 j 栋房子建立 i 个邮局时的最优解. 对于这个状态我们需要决策的就是 j 之前有多少栋房子共用第 i 个邮局, 故有:

```C++
f[i][j] = min{f[i - 1][j - x] + sumdis[j - x][j - 1]}
其中 sumdis[l][r] 表示下标范围为 [l, r] 的房子之间建立一个邮局, 这些房子与该邮局的最短距离
(注意f[i][j]中的j表示的第j栋房子从1计数, sumdis从0计数)
```

sumdis数组可以实现预处理出来, 具体算法与中位数的性质有关. 即对于 sumdis[l][r], 直接选择这 r - l + 1 栋房子中, 中间的那一栋建立邮局(如果是偶数栋, 中间的两栋任选一栋), 这时这些房子与邮局的距离之和是最短的.

至于dp的边界: f[i][0] = 0, f[0][j] = INF, 以及 i >= j 时 f[i][j] = 0

另外, 这样的状态定义可以用滚动数组优化空间.
```cpp
class Solution {
public:
    /**
     * @param A: an integer array
     * @param k: An integer
     * @return: an integer
     */
    int postOffice(vector<int> &A, int k) {
        int n = A.size();
        if (n <= k) {
            return 0;
        }
        
        vector<vector<int>> f(k + 1, vector<int>(n + 1, 0x3f3f3f3f));
        vector<vector<int>> sumdis(n, vector<int>(n, 0));
        
        sort(A.begin(), A.end());
        
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int pos = A[(i + j) / 2];
                for (int k = i; k <= j; k++) {
                    sumdis[i][j] += abs(A[k] - pos);
                }
            }
        }
        
        for (int i = 0; i <= k; i++) {
            for (int j = 0; j <= i; j++) {
                f[i][j] = 0;
            }
        }
        
        for (int i = 1; i <= k; i++) {
            for (int j = i + 1; j <= n; j++) {
                for (int x = 1; x <= j; x++) {
                    f[i][j] = min(f[i][j], f[i - 1][j - x] + sumdis[j - x][j - 1]);
                }
            }
        }
        
        return f[k][n];
    }
};

class Solution {
public:
    /**
     * @param A an integer array
     * @param k an integer
     * @return an integer
     */
    int N, P;
    int f[1500][1500], w[1500][1500], a[1500], K[1500][1500];
	vector<int> tmp;
    void init() {
        int n = tmp.size();
        a[0] = 0;
        for (int i = 1; i <= n; i ++) {
            a[i] = a[i - 1] + tmp[i-1];
        }
    }

    int getw(int x, int y)  {
        int t = (x + y) / 2;
        return a[y] - a[t] - (y - t) * tmp[t - 1] + (t - x) * tmp[t - 1] - (a[t - 1] - a[x - 1]);
    }

    void solve(int N, int P) {
        for (int i = 0; i <= N; i ++) {
            f[i][i] = 0;
            K[i][i] = i;
        }
		int j;
        for (int p = 1; p <= N - P; p ++) {
            for (int i = 0; (j  = i + p) <= N; i ++)
                f[i][j] = 0x7fffffff / 3;
            int t;
            for (int i = 1; (j = i + p) <= N; i ++) {
                for (int k = K[i][j - 1]; k <= K[i + 1][j]; k ++)
                    if ((t = f[i - 1][k - 1] + getw(k, j)) < f[i][j]) {
                        f[i][j] = t;
                        K[i][j] = k;
                    }
            }
        }
    }

    void getAns(int k, int r, vector<int>& ret) {
        if ( k == 0 || r <= 0)
            return;
        int p = K[k][r];
        getAns(k - 1, p - 1, ret);
        ret.push_back(tmp[(p + r) / 2 - 1]);
    }

    int postOffice(vector<int>& A, int k) {
        // Write your code here
        sort(A.begin(), A.end());
		tmp = A;
        int n = A.size();
        init();
        solve(n, k);

        vector<int> result;
        getAns(k, n, result);
        return f[k][n];
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)