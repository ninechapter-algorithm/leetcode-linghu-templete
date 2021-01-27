# 子数组的最大平均值 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-average-subarray-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个整数数组，有正有负。找到这样一个子数组，他的长度大于等于 `k`，且平均值最大。
 ### 样例说明
 例1:
```
输入:
[1,12,-5,-6,50,3]
3
输出:
15.667
解释:
 (-6 + 50 + 3) / 3 = 15.667
```

例2:
```
输入:
[5]
1
输出:
5.000
```



 ### 参考代码
 使用九章算法强化班中讲过的基于二分答案的方法
二分出 average 之后，把数组中的每个数都减去 average，然后的任务就是去求这个数组中，是否有长度 >= k 的 subarray，他的和超过 0。
这一步用类似 Maximum Subarray 的解法来做就好了
```java
// 九章算法强化班版本，辅助空间O(1) 
public class Solution {
    /**
     * @param nums: an array with positive and negative numbers
     * @param k: an integer
     * @return: the maximum average
     */
    
    private boolean canFind(int[] A, int K, double avg) {
        int i, k;
        double rightSum = 0, leftSum = 0, minLeftSum = 0;
        for (i = 0; i < K; ++i) {
            rightSum += A[i] - avg;
        }
        
        for (i = K; i <= A.length; ++i) {
            if (rightSum - minLeftSum >= 0) {
                return true;
            }
            
            if (i < A.length) {
                rightSum += A[i] - avg;
                leftSum += A[i - K] - avg;
                minLeftSum = Math.min(minLeftSum, leftSum);
            }
        }
        
        return false;
    } 
     
    public double maxAverage(int[] A, int K) {
        int i;
        double start, stop, mid;
        start = stop = A[0];
        for (i = 0; i < A.length; ++i) {
            start = Math.min(A[i], start);
            stop = Math.max(A[i], stop);
        }
        
        while (start + 1e-5 < stop) {
            mid = (start + stop) / 2;
            if (canFind(A, K, mid)) {
                start = mid;
            }
            else {
                stop = mid;
            }
        }
        
        return start;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)