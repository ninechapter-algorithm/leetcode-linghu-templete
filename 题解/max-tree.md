# 最大树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/max-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个没有重复的整数数组，在此数组上建立最大树的定义如下：

- 根是数组中最大的数
- 左子树和右子树元素分别是被父节点元素切分开的子数组中的最大值

利用给定的数组构造最大树。
 ### 样例说明
 **样例 1:**
```
输入：[2, 5, 6, 0, 3, 1]
输出：{6,5,3,2,#,0,1}
解释：
此数组构造的最大树是：
```
        6
       / \
      5   3
     /   / \
    2   0   1
```
```
**样例 2:**
```
输入：[6,4,20]
输出：{20,6,#,#,4}
解释：
     20
     / 
    6
     \
      4

```
 ### 参考代码
 使用九章算法强化班中讲到的单调栈。保存一个单调递减栈。每个数从栈中被 pop 出的时候，就知道它往左和往右的第一个比他大的数的位置了。
时间复杂度 $O(n)$，而暴力算法最坏情况下会有 $O(n^2)$
```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    """
    @param A: Given an integer array with no duplicates.
    @return: The root of max tree.
    """
    def maxTree(self, A):
        if not A:
            return None
            
        nodes = [TreeNode(num) for num in A + [sys.maxsize]]
        stack = []
        for index, num in enumerate(A + [sys.maxsize]):
            while stack and A[stack[-1]] < num:
                top = stack.pop()
                left = A[stack[-1]] if stack else sys.maxsize
                if left < num:
                    nodes[stack[-1]].right = nodes[top]
                else:
                    nodes[index].left = nodes[top]
            
            stack.append(index)

        # sys.maxsize 's left child is the maximum number
        return nodes[-1].left
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)