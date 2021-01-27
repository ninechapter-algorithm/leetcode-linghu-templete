# 无序数组K小元素
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/kth-smallest-numbers-in-unsorted-array/?utm_source=sc-github-wzz)
 ## 题目描述
 找到一个无序数组中第K小的数
 ### 样例说明
 **样例 1:**

```
输入: [3, 4, 1, 2, 5], k = 3
输出: 3
```

**样例 2:**

```
输入: [1, 1, 1], k = 2
输出: 1
```
 ### 参考代码
 Quick Select 快速选择算法的模板题. 与快速排序过程相似.

维基百科: <https://zh.wikipedia.org/wiki/%E5%BF%AB%E9%80%9F%E9%80%89%E6%8B%A9>
```java
class Solution {
    /*
     * @param k an integer
     * @param nums an integer array
     * @return kth smallest element
     */
    public int kthSmallest(int k, int[] nums) {
        return quickSelect(nums, 0, nums.length - 1, k - 1);
    }

    public int quickSelect(int[] A, int start, int end , int k) {
        if (start == end)
            return A[start];
        
        int left = start, right = end;
        int pivot = A[(start + end) / 2];

        while (left <= right) {
            while (left <= right && A[left] < pivot) {
                left++;
            }
            while (left <= right && A[right] > pivot) {
                right--;
            }
            if (left <= right) {
                int temp = A[left];
                A[left] = A[right];
                A[right] = temp;
                
                left++;
                right--;
            }
        }

        if (right >= k && start <= right)
            return quickSelect(A, start, right, k);
        else if (left <= k && left <= end)
            return quickSelect(A, left, end, k);
        else
            return A[k];
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)