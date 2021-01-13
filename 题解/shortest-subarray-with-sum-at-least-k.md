# 和至少为 K 的最短子数组
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/shortest-subarray-with-sum-at-least-k/?utm_source=sc-github-wzz)
 ## 题目描述
 返回 `A` 的最短的非空连续子数组的**长度**，该子数组的和至少为 `K` 。

如果没有和至少为 `K` 的非空子数组，返回 `-1` 。
 ### 样例说明
 **样例 1:**
```
输入：A = [1], K = 1
输出：1
```
**样例 2:**
```
输入：A = [1,2], K = 4
输出：-1
```
 ### 参考代码
 使用堆的方法。堆支持删除的时候用 lazy_deletion 的方法。
解题详情详见《九章算法面试高频题班》中的讲解

```
[[python]]
from heapq import heappush, heappop


class Heap:
    
    def __init__(self):
        self.minheap = []
        self.deleted_set = set()
    
    def push(self, index, val):
        heappush(self.minheap, (val, index))
    
    def _lazy_deletion(self):
        while self.minheap and self.minheap[0][1] in self.deleted_set:
            heappop(self.minheap)
    
    def top(self):
        self._lazy_deletion()
        return self.minheap[0]
    
    def pop(self):
        self._lazy_deletion()
        heappop(self.minheap)
        
    def delete(self, index):
        self.deleted_set.add(index)
        
    def is_empty(self):
        return not bool(self.minheap)
        

class Solution:
    """
    @param A: the array
    @param K: sum
    @return: the length
    """
    def shortestSubarray(self, A, K):
        prefix_sum = self.get_prefix_sum(A)
        
        # do binary search to find the minimum length that
        # we could find a subarray within that length and sum >= K
        start, end = 1, len(A)
        while start + 1 < end:
            mid = (start + end) // 2
            if self.is_valid(prefix_sum, K, mid):
                end = mid
            else:
                start = mid
        if self.is_valid(prefix_sum, K, start):
            return start
        if self.is_valid(prefix_sum, K, end):
            return end
        return -1
    
    def is_valid(self, prefix_sum, K, length):
        minheap = Heap()
        for end in range(len(prefix_sum)):
            index = end - length - 1
            minheap.delete(index)
            # find the maximum subarray
            if not minheap.is_empty() and prefix_sum[end] - minheap.top()[0] >= K:
                return True
            minheap.push(end, prefix_sum[end])
        return False
        
    def get_prefix_sum(self, A):
        prefix_sum = [0]
        for num in A:
            prefix_sum.append(prefix_sum[-1] + num)
        return prefix_sum
[[java]]
class ValueIndexPair {
    int val, index;
    public ValueIndexPair(int val, int index) {
        this.val = val;
        this.index = index;
    } 
}

class Heap {
    private Queue<ValueIndexPair> minheap;
    private Set<Integer> deleteSet;
    public Heap() {
        minheap = new PriorityQueue<>((p1, p2) -> (p1.val - p2.val));
        deleteSet = new HashSet<>();
    }
    
    public void push(int index, int val) {
        minheap.add(new ValueIndexPair(val, index));
    }
    
    private void lazyDeletion() {
        while (minheap.size() != 0 && deleteSet.contains(minheap.peek().index)) {
            ValueIndexPair pair = minheap.poll();
            deleteSet.remove(pair.index);
        }
    }
    
    public ValueIndexPair top() {
        lazyDeletion();
        return minheap.peek();
    }
    
    public void pop() {
        lazyDeletion();
        minheap.poll();
    }
    
    public void delete(int index) {
        deleteSet.add(index);
    }
    
    public boolean isEmpty() {
        return minheap.size() == 0;
    }
}

public class Solution {
    /**
     * @param A: the array
     * @param K: sum
     * @return: the length
     */
    public int shortestSubarray(int[] A, int K) {
        int[] prefixSum = getPrefixSum(A);
        
        int start = 1, end = A.length;
        while (start + 1 < end) {
            int mid = (start + end) / 2;
            if (isValid(prefixSum, K, mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (isValid(prefixSum, K, start)) {
            return start;
        }
        if (isValid(prefixSum, K, end)) {
            return end;
        }
        return -1;
    }
    
    private boolean isValid(int[] prefixSum, int K, int length) {
        Heap minheap = new Heap();
        for (int end = 0; end < prefixSum.length; end++) {
            int index = end - length - 1;
            minheap.delete(index);
            if (!minheap.isEmpty() && prefixSum[end] - minheap.top().val >= K) {
                return true;
            }
            minheap.push(end, prefixSum[end]);
        }
        return false;
    }
    
    private int[] getPrefixSum(int[] A) {
        int[] prefixSum = new int[A.length + 1];
        prefixSum[0] = 0;
        for (int i = 0; i < A.length; i++) {
            prefixSum[i + 1] = prefixSum[i] + A[i];
        }
        return prefixSum;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)