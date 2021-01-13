# 最大子数组 V
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-subarray-v/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个整数数组，找到长度在 `k1` 与 `k2` 之间(包括 k1, k2)的子数组并且使它们的和最大，返回这个最大值，如果数组元素个数小于 k1 则返回 0
 ### 样例说明
 **样例 1:**
```
输入:
[-2,2,-3,4,-1,2,1,-5,3]
2
4
输出:
6

解释:
连续子数组为 `[4,-1,2,1]` 时有最大和 `6`
```

**样例 2:**
```
输入:
[1,1,2,3]
5
10
输出:
0
```
 ### 参考代码
 滑动窗口系列题，deque维护子数组，每一次窗口滑动则：前缀和 - 队头，最后得出最大值。
```java
public class Solution {
    /**
     * @param nums an array of integers
     * @param k1 an integer
     * @param k2 an integer
     * @return the largest sum
     */
    public int maxSubarray5(int[] nums, int k1, int k2) {
        // Write your code here
        int n = nums.length;
        if (n < k1)
            return 0;

        int result = Integer.MIN_VALUE;

        int[] sum = new int[n + 1];
        sum[0] = 0;
        LinkedList<Integer> queue = new LinkedList<Integer>();

        for (int i = 1; i <= n; ++i) {
            sum[i] = sum[i - 1] + nums[i - 1];

            if (!queue.isEmpty() && queue.getFirst() < i - k2) {
                queue.removeFirst();
            }
            if (i >= k1) {
                while (!queue.isEmpty() && sum[queue.getLast()] > sum[i - k1]) {
                    queue.removeLast();
                }
                queue.add(i - k1);
            }

            // [i - k2, i - k1]
            if (!queue.isEmpty() && sum[i] - sum[queue.getFirst()] > result) {
                result = Math.max(result, sum[i] - sum[queue.getFirst()]);
            }


        }
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)