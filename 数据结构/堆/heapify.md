# 堆化
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/heapify/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个整数数组，堆化操作就是把它变成一个最小堆数组。

对于堆数组A，A[0]是堆的根，并对于每个A[i]，A [i * 2 + 1]是A[i]的左儿子并且A[i * 2 + 2]是A[i]的右儿子。

 ### 样例说明
 ***样例 1***
```
输入 : [3,2,1,4,5]
输出 : [1,2,3,4,5]
解释 : 返回任何一个合法的堆数组
```
 ### 参考代码
 Heapify 的具体实现方法。时间复杂度为 $O(n)$，使用的是 siftdown
之所以是 O(n) 是因为从第 N/2 个位置开始往下 siftdown，那么就有大约 N/4 个数在 siftdown 中最多交换 1 次，N/8 个数最多交换 2 次，N/16 个数最多交换 3 次。
所以 $O(N/4 * 1 + N/8 * 2 + N/16 * 3 + ... + 1 * LogN) = O(N)$
```python
class Solution:
    """
    @param: A: Given an integer array
    @return: nothing
    """
    def heapify(self, A):
        for i in range(len(A) // 2, -1, -1):
            self.siftdown(A, i)
            
    def siftdown(self, A, index):
        n = len(A)
        while index < n:
            left = index * 2 + 1
            right = index * 2 + 2
            minIndex = index
            if left < n and A[left] < A[minIndex]:
                minIndex = left
            if right < n and A[right] < A[minIndex]:
                minIndex = right

            if minIndex == index:
                break
            
            A[minIndex], A[index] = A[index], A[minIndex]
            index = minIndex
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)