# 第K大的元素 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/kth-largest-element-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 找到数组中第K大的元素，N远大于K。请注意你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素
 ### 样例说明
 **例1:**
```
输入:[9,3,2,4,8],3
输出:4

```
**例2:**
```
输入:[1,2,3,4,5,6,8,9,10,7],10
输出:1

```

 ### 参考代码
 利用优先队列求第k大元素
```java
class Solution {
    /**
     * @param nums an integer unsorted array
     * @param k an integer from 1 to n
     * @return the kth largest element
     */
    public int kthLargestElement2(int[] nums, int k) {
        // Write your code here
        PriorityQueue<Integer> q = new PriorityQueue<Integer>(k);
        for (int num : nums) {
            q.offer(num);
            if (q.size() > k) {
                q.poll();
            }
        }
        return q.peek();
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)