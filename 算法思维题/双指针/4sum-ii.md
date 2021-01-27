# 4数和 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/4sum-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给出 A, B, C, D 四个整数列表，计算有多少的tuple `(i, j, k, l)`满足`A[i] + B[j] + C[k] + D[l]`为 0。

为了简化问题，A, B, C, D 具有相同的长度，且长度N满足 0 ≤ N ≤ 500。所有的整数都在范围(-2^28, 2^28 - 1)内以及保证结果最多为2^31 - 1。
 ### 样例说明
 例1:
```
输入:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

输出:
2

解释:
这两个tuple为:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
```
例2:
```
输入:
A = [0]
B = [0]
C = [0]
D = [0]

输出:
1
```

 ### 参考代码
 时间复杂度和空间复杂度均为 $O(N^2)$
将 a,b 组成的和及其组成方案个数统计在hash里，然后再去枚举 c,d 的组合，然后找 -(c+d) 在 hash 里的组合数。
```
[[python]]
class Solution:
    """
    @param A: a list
    @param B: a list
    @param C: a list
    @param D: a list
    @return: how many tuples (i, j, k, l) there are such that A[i] + B[j] + C[k] + D[l] is zero
    """
    def fourSumCount(self, A, B, C, D):
        counter = {}
        for a in A:
            for b in B:
                counter[a + b] = counter.get(a + b, 0) + 1
        answer = 0
        for c in C:
            for d in D:
                answer += counter.get(-c - d, 0)
        return answer
[[java]]
public class Solution {
    /**
     * @param A: a list
     * @param B: a list
     * @param C: a list
     * @param D: a list
     * @return: how many tuples (i, j, k, l) there are such that A[i] + B[j] + C[k] + D[l] is zero
     */
    public int fourSumCount(int[] A, int[] B, int[] C, int[] D) {
        Map<Integer, Integer> counter = new HashMap<>();
        for (int i = 0; i < A.length; i++) {
            for (int j = 0; j < B.length; j++) {
                int sum = A[i] + B[j];
                counter.put(sum, counter.getOrDefault(sum, 0) + 1);
            }
        }
        
        int answer = 0;
        for (int i = 0; i < C.length; i++) {
            for (int j = 0; j < D.length; j++) {
                int sum = C[i] + D[j];
                answer += counter.getOrDefault(-sum, 0);
            }
        }
        return answer;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)