# 等差切片 II - 子序列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/arithmetic-slices-ii-subsequence/?utm_source=sc-github-wzz)
 ## 题目描述
 如果一个数字序列由至少三个元素组成, 并且任何两个相邻元素之间的差值相同, 则称之为等差数列.

比如, 下面这些就是等差数列:
```
1,  3,  5,  7,  9
7,  7,  7,  7
3, -1, -5, -9
```
而下面这个序列就不是等差的:
```
1, 1, 2, 5, 7
```

给定一个数组 `A`, 它的长度为 `N`. 对于任意 `A[P0], A[P1], ..., A[Pk]`, 如果它满足 `0 ≤ P0 < P1 < ... < Pk < N`, 则称它为 `A` 的一个子序列切片.

如果 `A[P0], A[P1], ..., A[Pk]` 是等差的, 则称它是 `A` 的一个等差切片. 注意, 这意味着 k ≥ 2.

返回 `A` 中等差切片的数量.
 ### 样例说明
 **样例 1:**

```
输入: [2, 4, 6, 8, 10]
输出: 7
解释: 
    所有的等差切片为:
    [2, 4, 6] 
    [4, 6, 8] 
    [2, 6, 10]
    [6, 8, 10]
    [2, 4, 6, 8]
    [4, 6, 8, 10]
    [2, 4, 6, 8, 10]
```

**样例 2:**

```
输入: [1, 2, 3]
输出: 1
解释: 只有 [1, 2, 3]
```
 ### 参考代码
 设定状态:

```
f[i][d]  表示以 A 中下标为 i 的数结尾的, 公差为 d 的等差切片的数量
f2[i][d] 表示以 A 中下标为 i 的数结尾的, 长度为 2 的, 公差为 d 的等差切片的数量
(f2记录的严格来说并不能称为等差切片, 因为长度小于 3, 只是为了描述方便)
```

状态转移:

```C++
对于 i, 枚举 0 <= j < i, d = A[i] - A[j]
f[i][d] += f2[j][d] + f[j][d]   // 以 j 结尾的长度为2的等差切片, 增加了 A[i] 就会变成真正的等差切片
f2[i][d] += 1                   // A[j], A[i] 组成一个长度为 2 的等差切片
```

最后答案就是 f 内所有整数的和. 由于公差 d 可能是负数, 可能非常大而且不连续, 所以我们采用哈希表存储.
```java
public class Solution {
    public int numberOfArithmeticSlices(int[] A) {
        if (A == null || A.length < 3) {
            return 0;
        }
        int N = A.length;
        Map<Integer, Integer>[] f = new Map[N];
        Map<Integer, Integer>[] f2 = new Map[N];
        int ans = 0;
        for (int i = 0; i < N; i++) {
            f[i] = new HashMap<>();
            f2[i] = new HashMap<>();
            for (int j = 0; j < i; j++) {
                if (Math.abs((long)A[i] - A[j]) > Integer.MAX_VALUE) {
                    continue;
                }
                int d = A[i] - A[j];
                
                int f2_j_d = f2[j].getOrDefault(d, 0);
                int f_j_d = f[j].getOrDefault(d, 0);
                int f_i_d = f[i].getOrDefault(d, 0);
                f[i].put(d, f_i_d + f_j_d + f2_j_d);
                
                int f2_i_d = f2[i].getOrDefault(d, 0);
                f2[i].put(d, f2_i_d + 1);
            }
            
            for (Integer o : f[i].keySet()) {
                ans += f[i].get(o);
            }
        }
        return ans;
    }
}

// version2: 更简洁的写法
public class Solution {
    public int numberOfArithmeticSlices(int[] A) {
        if (A == null || A.length < 3) {
            return 0;
        }
        Map<Integer, Integer>[] map = new Map[A.length];
        int ans = 0;
        for (int i = 0; i < A.length; i++) {
            map[i] = new HashMap<>();
            for (int j = 0; j < i; j++) {
                if (Math.abs((long)A[i] - A[j]) > Integer.MAX_VALUE) {
                    continue;
                }
                int d = A[i] - A[j];
                int map_i_d = map[i].getOrDefault(d, 0);
                int map_j_d = map[j].getOrDefault(d, 0);
                map_i_d += map_j_d + 1;
                map[i].put(d, map_i_d);
                ans += map_j_d;
            }
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)