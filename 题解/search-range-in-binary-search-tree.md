# 二叉查找树中搜索区间
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/search-range-in-binary-search-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二叉查找树和范围`[k1, k2]`。按照升序返回给定范围内的节点值。
 ### 样例说明
 **样例 1:**
```
输入：{5},6,10
输出：[]
        5
它将被序列化为 {5}
没有数字介于6和10之间
```
**样例 2:**
```
输入：{20,8,22,4,12},10,22
输出：[12,20,22]
解释：
        20
       /  \
      8   22
     / \
    4   12
它将被序列化为 {20,8,22,4,12}
[12,20,22]介于10和22之间
```
 ### 参考代码
 http://lintcode.com/zh-cn/problem/search-range-in-binary-search-tree/


考点：
* 二叉查找树 ：
二叉排序树或者是一棵空树，或者是具有下列性质的二叉树：
（1）若左子树不空，则左子树上所有结点的值均小于它的根结点的值；
（2）若右子树不空，则右子树上所有结点的值均大于或等于它的根结点的值；
（3）左、右子树也分别为二叉排序树；

题解：从给定的BST的根节点开始查找，如果位于[k1,k2]，存入结果，向左右子树分别搜索。
```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        this.val = val
        this.left, this.right = None, None
"""
class Solution:
    """
    @param root: The root of the binary search tree.
    @param k1 and k2: range k1 to k2.
    @return: Return all keys that k1<=key<=k2 in increasing order.
    """     
    def searchRange(self, root, k1, k2):
        # write your code here
        ans = []
        if root is None:
            return ans
        queue = [root]
        index = 0
        while index < len(queue):
            if queue[index] is not None:
                if queue[index].val >= k1 and \
                    queue[index].val <= k2:
                    ans.append(queue[index].val)

                queue.append(queue[index].left)
                queue.append(queue[index].right)

            index += 1
        return sorted(ans)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)