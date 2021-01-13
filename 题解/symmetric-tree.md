# 对称树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/symmetric-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给定二叉树，返回它是否是自身的镜像（即这棵二叉树是否对称）。
 ### 样例说明
 **样例1**

```
输入: {1,2,2,3,4,4,3}
输出: true
解释:
    1
   / \
  2   2
 / \ / \
3  4 4  3
{1,2,2,3,4,4,3}这棵二叉树是对称的
```

**样例2**

```
输入: {1,2,2,#,3,#,3}
输出: false
解释:
    1
   / \
  2   2
   \   \
   3    3
很显然这棵二叉树并不对称
```

 ### 参考代码
 使用分治法 Divide Conquer 的版本

```
[[python]]
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    """
    @param root: root of the given tree
    @return: whether it is a mirror of itself 
    """
    def isSymmetric(self, root):
        if not root:
            return True
        return self._is_symmetric(root.left, root.right)
        
    def _is_symmetric(self, left_root, right_root):
        if left_root is None and right_root is None:
            return True
        if left_root is None or right_root is None:
            return False
        if left_root.val != right_root.val:
            return False
            
        left = self._is_symmetric(left_root.left, right_root.right)
        right = self._is_symmetric(left_root.right, right_root.left)
        return left and right

[[java]]
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param root: root of the given tree
     * @return: whether it is a mirror of itself 
     */
    public boolean isSymmetric(TreeNode root) {
        // Write your code here
        if (root == null) {
            return true;
        }
        
        return isSymmetric(root.left, root.right);
    }
    
    private boolean isSymmetric(TreeNode leftRoot, TreeNode rightRoot) {
        if (leftRoot == null && rightRoot == null) {
            return true;
        }
        if (leftRoot == null || rightRoot == null) {
            return false;
        }
        if (leftRoot.val != rightRoot.val) {
            return false;
        }
        
        boolean left = isSymmetric(leftRoot.left, rightRoot.right);
        boolean right = isSymmetric(leftRoot.right, rightRoot.left);
        
        return left && right;
    }
}
```

使用Iteration的版本
```
[[python]]
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    """
    @param root: root of the given tree
    @return: whether it is a mirror of itself 
    """
    
    def isSymmetric(self, root):
        inorder = self.inorder(root, reverse=False)
        reverse_inorder = self.inorder(root, reverse=True)
        if inorder != reverse_inorder:
            return False
            
        preorder = self.preorder(root, reverse=False)
        reverse_preorder = self.preorder(root, reverse=True)
        return preorder == reverse_preorder
        
    def get_left(self, node, reverse):
        if reverse:
            return node.right
        return node.left
        
    def get_right(self, node, reverse):
        if reverse:
            return node.left
        return node.right
        
    def preorder(self, root, reverse):
        stack = [root]
        order = []
        while stack:
            node = stack.pop()
            order.append(node.val)
            right = self.get_right(node, reverse)
            if right:
                stack.append(right)
            left = self.get_left(node, reverse)
            if left:
                stack.append(left)
        return order
        
    def inorder(self, root, reverse):
        stack = []
        while root is not None:
            stack.append(root)
            root = self.get_left(root, reverse)
            
        order = []
        while stack:
            node = stack[-1]
            order.append(node.val)
            right = self.get_right(node, reverse)
            if right is not None:
                node = right
                while node is not None:
                    stack.append(node)
                    node = self.get_left(node, reverse)
            else:
                stack.pop()
                while stack and self.get_right(stack[-1], reverse) == node:
                    node = stack.pop()
        
        return order
[[java]]
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param root: root of the given tree
     * @return: whether it is a mirror of itself 
     */
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        
        List<Integer> inorder = inorder(root, false);
        List<Integer> reverseInorder = inorder(root, true);
        for (int i = 0; i < inorder.size(); i++) {
            if (inorder.get(i) != reverseInorder.get(i)) {
                return false;
            }
        }
        
        List<Integer> preorder = this.preorder(root, false);
        List<Integer> reversePreorder = this.preorder(root, true);
        for (int i = 0; i < preorder.size(); i++) {
            if (preorder.get(i) != reversePreorder.get(i)) {
                return false;
            }
        }
        
        return true;
    }
    
    private TreeNode getLeft(TreeNode node, boolean reverse) {
        if (reverse) {
            return node.right;
        }
        return node.left;
    }
    
    private TreeNode getRight(TreeNode node, boolean reverse) {
        if (reverse) {
            return node.left;
        }
        return node.right;
    }
    
    private List<Integer> preorder(TreeNode root, boolean reverse) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> order = new ArrayList<>();
        stack.push(root);
        
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            order.add(node.val);
            TreeNode right = getRight(node, reverse);
            if (right != null) {
                stack.push(right);
            }
            TreeNode left = getLeft(node, reverse);
            if (left != null) {
                stack.push(left);
            }
        }
        
        return order;
    }
    
    private List<Integer> inorder(TreeNode root, boolean reverse) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> order = new ArrayList<>();
        
        while (root != null) {
            stack.push(root);
            root = getLeft(root, reverse);
        }
        
        while (!stack.isEmpty()) {
            TreeNode node = stack.peek();
            order.add(node.val);
            TreeNode right = getRight(node, reverse);
            if (right != null) {
                node = right;
                while (node != null) {
                    stack.push(node);
                    node = getLeft(node, reverse);
                }
            } else {
                stack.pop();
                while (!stack.isEmpty() && getRight(stack.peek(), reverse) == node) {
                    node = stack.pop();
                }
            }
        }
        
        return order;
    }
}
```

使用 BFS 算法的版本
```
[[python]]
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    """
    @param root: root of the given tree
    @return: whether it is a mirror of itself 
    """
    def isSymmetric(self, root):
        queue = [root]
        while queue:
            next_queue = []
            for i in range(len(queue)):
                if queue[i] is None:
                    continue
                next_queue.append(queue[i].left)
                next_queue.append(queue[i].right)
            if not self.is_mirror(next_queue):
                return False
            queue = next_queue
        return True
        
    def is_mirror(self, queue):
        left, right = 0, len(queue) - 1
        while left < right:
            if not self.is_same(queue[left], queue[right]):
                return False
            left, right = left + 1, right - 1
        return True
        
    def is_same(self, node1, node2):
        if node1 and node2:
            return node1.val == node2.val
        return node1 is None and node2 is None
[[java]]
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param root: root of the given tree
     * @return: whether it is a mirror of itself 
     */
    public boolean isSymmetric(TreeNode root) {
        List<TreeNode> queue = new ArrayList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            List<TreeNode> nextQueue = new ArrayList<>();
            for (int i = 0; i < queue.size(); i++) {
                if (queue.get(i) == null) {
                    continue;
                }
                nextQueue.add(queue.get(i).left);
                nextQueue.add(queue.get(i).right);
            }
            if (!isMirror(nextQueue)) {
                return false;
            }
            queue = nextQueue;
        }
        return true;
    }
    
    private boolean isMirror(List<TreeNode> queue) {
        int left = 0, right = queue.size() - 1;
        while (left < right) {
            if (!isSame(queue.get(left), queue.get(right))) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
    
    private boolean isSame(TreeNode node1, TreeNode node2) {
        if (node1 != null && node2 != null) {
            return node1.val == node2.val;
        }
        return node1 == null && node2 == null;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)