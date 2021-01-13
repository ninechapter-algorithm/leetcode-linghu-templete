# 将二叉树按照层级转化为链表
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/convert-binary-tree-to-linked-lists-by-depth/?utm_source=sc-github-wzz)
 ## 题目描述
 给一棵二叉树，设计一个算法为每一层的节点建立一个链表。也就是说，如果一棵二叉树有 `D` 层，那么你需要创建 `D` 条链表。

 ### 样例说明
 **样例 1:**

```
输入: {1,2,3,4}
输出: [1->null,2->3->null,4->null]
解释: 
        1
       / \
      2   3
     /
    4
```

**样例 2:**

```
输入: {1,#,2,3}
输出: [1->null,2->null,3->null]
解释: 
    1
     \
      2
     /
    3
```
 ### 参考代码
 考点：
* 搜索遍历

题解：采用基本的bfs搜索实现层序遍历即可。分别使用DFS和BFS两种解法解决这个问题。时间复杂度都是O(n)。
```python
# BFS 解法
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        this.val = val
        this.left, this.right = None, None
Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
"""
class Solution:
    # @param {TreeNode} root the root of binary tree
    # @return {ListNode[]} a lists of linked list
    def binaryTreeToLists(self, root):
        result = []
        if root is None:
            return result
            
        import Queue
        queue = Queue.Queue()
        
        queue.put(root)
        
        dummy = ListNode(0)
        
        lastNode = None
        
        while not queue.empty():
            dummy.next = None
            lastNode = dummy
            size = queue.qsize()
            for i in xrange(size):
                head = queue.get()
                lastNode.next = ListNode(head.val)
                lastNode = lastNode.next

                if head.left is not None:
                    queue.put(head.left)
                if head.right is not None:
                    queue.put(head.right)
        
            result.append(dummy.next)
        
        return result
    


# DFS 解法

"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        this.val = val
        this.left, this.right = None, None
Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
"""
class Solution:
    # @param {TreeNode} root the root of binary tree
    # @return {ListNode[]} a lists of linked list
    def binaryTreeToLists(self, root):
        # Write your code here
        result = []
        self.dfs(root, 1, result)
        return result

    def dfs(self, root, depth, result):
        if root is None:
            return
        node = ListNode(root.val)
        if len(result) < depth:
            result.append(node)
        else:
            node.next = result[depth-1]
            result[depth-1] = node
        
        self.dfs(root.right, depth + 1, result)
        self.dfs(root.left, depth + 1, result)
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)