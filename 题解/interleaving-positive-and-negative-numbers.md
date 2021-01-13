# 交错正负数
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/interleaving-positive-and-negative-numbers/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个含有正整数和负整数的数组，重新排列成一个正负数交错的数组。

 ### 样例说明
 ***样例 1***
```
输入 : [-1, -2, -3, 4, 5, 6]
输出 : [-1, 5, -2, 4, -3, 6]
解释 : 或者仍和满足条件的答案 
```

 ### 参考代码
 先把正负数 partition 开，然后再相向双指针进行交换。
```
[[python]]
class Solution:
    """
    @param: A: An integer array.
    @return: nothing
    """
    def rerange(self, A):
        pos, neg = 0, 0
        for num in A:
            if num > 0:
                pos += 1
            else:
                neg += 1
        
        self.partition(A, pos > neg)
        self.interleave(A, pos == neg)
            
    def partition(self, A, start_positive):
        flag = 1 if start_positive else -1
        left, right = 0, len(A) - 1
        while left <= right:
            while left <= right and A[left] * flag > 0:
                left += 1
            while left <= right and A[right] * flag < 0:
                right -= 1
            if left <= right:
                A[left], A[right] = A[right], A[left]
                left += 1
                right -= 1
    
    def interleave(self, A, has_same_length):
        left, right = 1, len(A) - 1
        if has_same_length:
            right = len(A) - 2
            
        while left < right:
            A[left], A[right] = A[right], A[left]
            left, right = left + 2, right - 2
[[java]]
public class Solution {
    public void rerange(int[] A) {
        int pos = 0, neg = 0;
        for (int i = 0; i < A.length; i++) {
            if (A[i] > 0) {
                pos++;
            } else {
                neg++;
            }
        }
        
        partition(A, pos > neg);
        interleave(A, pos == neg);
    }
    
    private void partition(int[] A, boolean startPositive) {
        int flag = startPositive ? 1 : -1;
        int left = 0, right = A.length - 1;
        while (left <= right) {
            while (left <= right && A[left] * flag > 0) {
                left++;
            }
            while (left <= right && A[right] * flag < 0) {
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
    }
    
    private void interleave(int[] A, boolean has_same_length) {
        int left = 1, right = A.length - 1;
        if (has_same_length) {
            right = A.length - 2;
        }
        while (left < right) {
            int temp = A[left];
            A[left] = A[right];
            A[right] = temp;
            
            left += 2;
            right -= 2;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)