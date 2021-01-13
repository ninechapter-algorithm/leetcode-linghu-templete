# 木材加工
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/wood-cut/?utm_source=sc-github-wzz)
 ## 题目描述
 有一些原木，现在想把这些木头切割成一些长度相同的小段木头，需要得到的小段的数目至少为 `k`。当然，我们希望得到的小段越长越好，你需要计算能够得到的小段木头的最大长度。
 ### 样例说明
 **样例 1**

```plain
输入:
L = [232, 124, 456]
k = 7
输出: 114
Explanation: 我们可以把它分成114cm的7段，而115cm不可以
```

**样例 2**

```plain
输入:
L = [1, 2, 3]
k = 7
输出: 0
说明:很显然我们不能按照题目要求完成。
```
 ### 参考代码
 使用九章算法强化班中所讲的基于答案值域的二分法。
木头长度的范围在 1 到 max(L)，在这个范围内二分出一个长度 length，然后看看以这个 wood length 为前提的基础上，能切割出多少木头，如果少于 k 根，说明要短一些才行，如果多余 k，说明可以继续边长一些。
```python
class Solution:
    """
    @param L: Given n pieces of wood with length L[i]
    @param k: An integer
    @return: The maximum length of the small pieces
    """
    def woodCut(self, L, k):
        if not L:
            return 0

        start, end = 1, max(L)
        while start + 1 < end:
            mid = (start + end) // 2
            if self.get_pieces(L, mid) >= k:
                start = mid
            else:
                end = mid
                
        if self.get_pieces(L, end) >= k:
            return end
        if self.get_pieces(L, start) >= k:
            return start
            
        return 0
        
    def get_pieces(self, L, length):
        pieces = 0
        for l in L:
            pieces += l // length
        return pieces
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)