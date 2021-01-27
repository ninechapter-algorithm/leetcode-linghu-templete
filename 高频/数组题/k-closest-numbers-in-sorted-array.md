# 在排序数组中找最接近的K个数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/k-closest-numbers-in-sorted-array/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个目标数 `target`, 一个非负整数 `k`, 一个按照升序排列的数组 `A`。在`A`中找与`target`最接近的`k`个整数。返回这`k`个数并按照与`target`的接近程度从小到大排序，如果接近程度相当，那么小的数排在前面。
 ### 样例说明
 
 ### 参考代码
 直接在数组中二分查找 `target`, 如果不存在则返回大于 `target` 的最小的或者小于 `target` 的最大的元素均可.

然后使用两根指针从该位置开始向两端遍历, 每次把差值比较小的元素放入答案中然后将该指针向边界方向移动一下即可.
```java
public class Solution {
    /**
     * @param A      an integer array
     * @param target an integer
     * @param k      a non-negative integer
     * @return an integer array
     */
    public int[] kClosestNumbers(int[] A, int target, int k) {
        int[] result = new int[k];

        if (A == null || A.length == 0) {
            return A;
        }
        if (k > A.length) {
            return A;
        }

        int index = firstIndex(A, target);

        int start = index - 1;
        int end = index;
        for (int i = 0; i < k; i++) {
            if (start < 0) {
                result[i] = A[end++];
            } else if (end >= A.length) {
                result[i] = A[start--];
            } else {
                if (target - A[start] <= A[end] - target) {
                    result[i] = A[start--];
                } else {
                    result[i] = A[end++];
                }
            }
        }
        return result;
    }

    private int firstIndex(int[] A, int target) {
        int start = 0, end = A.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (A[mid] < target) {
                start = mid;
            } else if (A[mid] > target) {
                end = mid;
            } else {
                end = mid;
            }
        }

        if (A[start] >= target) {
            return start;
        }
        if (A[end] >= target) {
            return end;
        }
        return A.length;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)