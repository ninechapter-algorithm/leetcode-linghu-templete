# 二叉树的序列化和反序列化
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/serialize-and-deserialize-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 设计一个算法，并编写代码来序列化和反序列化二叉树。将树写入一个文件被称为“序列化”，读取文件后重建同样的二叉树被称为“反序列化”。

如何反序列化或序列化二叉树是没有限制的，你只需要确保可以将二叉树序列化为一个字符串，并且可以将字符串反序列化为原来的树结构。
 ### 样例说明
 
**样例 1：**
```
输入：{3,9,20,#,#,15,7}
输出：{3,9,20,#,#,15,7}
解释：
二叉树 {3,9,20,#,#,15,7}，表示如下的树结构：
	  3
	 / \
	9  20
	  /  \
	 15   7
它将被序列化为 {3,9,20,#,#,15,7}
```
**样例 2：**
```
输入：{1,2,3}
输出：{1,2,3}
解释：
二叉树 {1,2,3}，表示如下的树结构：
   1
  / \
 2   3
它将被序列化为 {1,2,3}
```
我们的数据是进行 BFS 遍历得到的。当你测试结果 Wrong Answer 时，你可以作为输入调试你的代码。

你可以采用其他的方法进行序列化和反序列化。
 ### 参考代码
 使用 BFS 的方法来 serialize
```python
from collections import deque

"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""


class Solution:
    """
    @param root: An object of TreeNode, denote the root of the binary tree.
    This method will be invoked first, you should design your own algorithm 
    to serialize a binary tree which denote by a root node to a string which
    can be easily deserialized by your own "deserialize" method later.
    """
    def serialize(self, root):
        if root is None:
            return ""
            
        # use bfs to serialize the tree
        queue = deque([root])
        bfs_order = []
        while queue:
            node = queue.popleft()
            bfs_order.append(str(node.val) if node else '#')
            if node:
                queue.append(node.left)
                queue.append(node.right)
            
        return ' '.join(bfs_order)

    """
    @param data: A string serialized by your serialize method.
    This method will be invoked second, the argument data is what exactly
    you serialized at method "serialize", that means the data is not given by
    system, it's given by your own serialize method. So the format of data is
    designed by yourself, and deserialize it here as you serialize it in 
    "serialize" method.
    """
    def deserialize(self, data):
        # None or ""
        if not data:
            return None

        bfs_order = [
            TreeNode(int(val)) if val != '#' else None
            for val in data.split()
        ]
        root = bfs_order[0]
        fast_index = 1
        
        nodes, slow_index = [root], 0
        while slow_index < len(nodes):
            node = nodes[slow_index]
            slow_index += 1
            node.left = bfs_order[fast_index]
            node.right = bfs_order[fast_index + 1]
            fast_index += 2
            
            if node.left:
                nodes.append(node.left)
            if node.right:
                nodes.append(node.right)
        
        return root
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)