# 最小差
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/the-smallest-difference/?utm_source=sc-github-wzz)
 ## 题目描述
 给定两个整数数组（第一个是数组 `A`，第二个是数组 `B`），在数组 A 中取 A[i]，数组 B 中取 B[j]，A[i] 和 B[j]两者的差越小越好(|A[i] - B[j]|), 返回最小差。
 ### 样例说明
 **样例 1:**

```
输入: A = [3, 6, 7, 4], B = [2, 8, 9, 3] 
输出: 0
解释: A[0] - B[3] = 0
```

**样例 2:**

```
输入: A = [1, 2, 3, 4], B = [7, 6, 5]
输出: 1
解释: B[2] - A[3] = 1
```
 ### 参考代码
 对A, B排序, 默认升序. 

设定两个指针开始遍历A, B, 每次向右移动值比较小的那个指针.

遍历过程中求差的绝对值, 更新答案. 时间复杂度O(*nlogn*)
```java
public class Solution {
    /**
     * @param A, B: Two integer arrays.
     * @return: Their smallest difference.
     */
    public int smallestDifference(int[] A, int[] B) {
        if (A == null || A.length == 0 || B == null || B.length == 0) {
            return 0;
        }
        
        Arrays.sort(A);
        Arrays.sort(B);
        
        int ai = 0, bi = 0;
        int min = Integer.MAX_VALUE;
        while (ai < A.length && bi < B.length) {
            min = Math.min(min, Math.abs(A[ai] - B[bi]));
            if (A[ai] < B[bi]) {
                ai++;
            } else {
                bi++;
            }
        }
        return min;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)