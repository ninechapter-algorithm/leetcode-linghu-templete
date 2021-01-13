# 找峰值 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/find-peak-element-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数矩阵 `A`, 它有如下特性:

- 相邻的整数不同
- 矩阵有 `n` 行 `m` 列。
- 对于所有的 `i < n`, 都有 `A[i][0] < A[i][1] && A[i][m - 2] > A[i][m - 1]`
- 对于所有的 `j < m`, 都有 `A[0][j] < A[1][j] && A[n - 2][j] > A[n - 1][j]`

我们定义一个位置 `[i,j]` 是峰值, 当且仅当它满足:

```C++
  A[i][j] > A[i + 1][j] && A[i][j] > A[i - 1][j] && 
  A[i][j] > A[i][j + 1] && A[i][j] > A[i][j - 1]
```

找到该矩阵的一个峰值元素, 返回它的坐标.
 ### 样例说明
 **样例 1:**

```
输入: 
    [
      [1, 2, 3, 6,  5],
      [16,41,23,22, 6],
      [15,17,24,21, 7],
      [14,18,19,20,10],
      [13,14,11,10, 9]
    ]
输出: [1,1]
解释: [2,2] 也是可以的. [1,1] 的元素是 41, 大于它四周的每一个元素 (2, 16, 23, 17).
```

**样例 2:**

```
输入: 
    [
      [1, 5, 3],
      [4,10, 9],
      [2, 8, 7]
    ]
输出: [1,1]
解释: 只有这一个峰值
```
 ### 参考代码
 网上很多 O(n+m) 的算法不正确, LintCode 已经加强数据.

正确的算法请参考: <http://courses.csail.mit.edu/6.006/spring11/lectures/lec02.pdf>
```java
// O(n + m) 解法
class Solution {
    /**
     * @param A: An integer matrix
     * @return: The index of the peak
     */
    public List<Integer> find(int x1, int x2, int y1, int y2, int[][] A) {

        int mid1 = x1 + (x2 - x1) / 2;
        int mid2 = y1 + (y2 - y1) / 2;

        int x = mid1, y = mid2;
        int max = A[mid1][mid2];
        for (int i = y1; i <= y2; ++i)
            if (A[mid1][i] > max) {
                max = A[mid1][i];
                x = mid1;
                y = i;
            }

        for (int i = x1; i <= x2; ++i)
            if (A[i][mid2] > max) {
                max = A[i][mid2];
                x = i;
                y = mid2;
            }

        boolean isPeak = true;
        if (A[x - 1][y] > A[x][y]) {
            isPeak = false;
            x -= 1;
        } else if (A[x + 1][y] > A[x][y]) {
            isPeak = false;
            x += 1;
        } else if (A[x][y - 1] > A[x][y]) {
            isPeak = false;
            y -= 1;
        } else if (A[x][y + 1] > A[x][y]) {
            isPeak = false;
            y += 1;
        }

        if (isPeak) {
            return new ArrayList<Integer>(Arrays.asList(x, y));
        }

        if (x >= x1 && x < mid1 && y >= y1 && y < mid2) {
            return find(x1, mid1 - 1, y1, mid2 - 1, A);
        }

        if (x >= 1 && x < mid1 && y > mid2 && y <= y2) {
            return find(x1, mid1 - 1, mid2 + 1, y2, A);
        }

        if (x > mid1 && x <= x2 && y >= y1 && y < mid2) {
            return find(mid1 + 1, x2, y1, mid2 - 1, A);
        }

        if (x >= mid1 && x <= x2 && y > mid2 && y <= y2) {
            return find(mid1 + 1, x2, mid2 + 1, y2, A);
        }

        return new ArrayList<Integer>(Arrays.asList(-1, -1));

    }

    public List<Integer> findPeakII(int[][] A) {
        // write your code here
        int n = A.length;
        int m = A[0].length;
        return find(1, n - 2, 1, m - 2, A);
    }
}

class Solution {
    /**
     * @param A: An integer matrix
     * @return: The index of the peak
     */
    public List<Integer> findPeakII(int[][] A) {
        // this is the nlog(n) method
        int low = 1, high = A.length - 2;
        List<Integer> ans = new ArrayList<Integer>();
        while (low <= high) {
            int mid = (low + high) / 2;
            int col = find(mid, A);
            if (A[mid][col] < A[mid - 1][col]) {
                high = mid - 1;
            } else if (A[mid][col] < A[mid + 1][col]) {
                low = mid + 1;
            } else {
                ans.add(mid);
                ans.add(col);
                break;
            }
        }
        return ans;
    }

    int find(int row, int[][] A) {
        int col = 0;
        for (int i = 0; i < A[row].length; i++) {
            if (A[row][i] > A[row][col]) {
                col = i;
            }
        }
        return col;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)