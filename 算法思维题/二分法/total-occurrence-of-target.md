# 目标出现总和
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/total-occurrence-of-target/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个升序的数组，以及一个*target*，找到它在数组中出现的次数。
 ### 样例说明
 样例1：
```
输入：[1,3,3,4,5]和target= 3，
输出：2。
```
样例2：
```
输入：[2,2,3,4,6]和target= 4，
输出：1。
```
样例3：
```
输入：[1,2,3,4,5]和target= 6，
输出：0。
```
 ### 参考代码
 用二分找到target 第一次出现的位置，在找到最后一次出现的位置，算一下距离差就知道了。
```java
public class Solution {
    /**
     * @param A an integer array sorted in ascending order
     * @param target an integer
     * @return an integer
     */
    public int totalOccurrence(int[] A, int target) {
        // Write your code here
        int n = A.length;
        if (n == 0) {
            return 0;
        }
        if (A[n-1] < target || A[0] > target) {
            return 0;
        }
        
        int l = 0, r = n - 1;
        int start = 0;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (A[mid] >= target) {
                start = mid;
                r = mid - 1;
            } else
                l = mid + 1;
        }
        if (A[start] != target)
            return 0;

        int end = n - 1;
        l = 0; r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (A[mid] <= target) {
                end = mid;
                l = mid + 1;
            } else
                r = mid - 1;
        }
        return end - start + 1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)