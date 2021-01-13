# 整数排序 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/sort-integers-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给一组整数，请将其在原地按照升序排序。使用归并排序，快速排序，堆排序或者任何其他 O(*n* log *n*) 的排序算法。
 ### 样例说明
 **例1：**
```
输入：[3,2,1,4,5]，
输出：[1,2,3,4,5]。
```
**例2：**
```
输入：[2,3,1]，
输出：[1,2,3]。
```
 ### 参考代码
 快速排序实现
```java
public class Solution {
    /**
     * @param A an integer array
     * @return void
     */
    public void sortIntegers2(int[] A) {
        quickSort(A, 0, A.length - 1);
    }
    
    private void quickSort(int[] A, int start, int end) {
        if (start >= end) {
            return;
        }
        
        int left = start, right = end;
        // key point 1: pivot is the value, not the index
        int pivot = A[(start + end) / 2];

        // key point 2: every time you compare left & right, it should be 
        // left <= right not left < right
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
        
        quickSort(A, start, right);
        quickSort(A, left, end);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)