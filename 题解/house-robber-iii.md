# 打劫房屋 III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/house-robber-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 在上次打劫完一条街道之后和一圈房屋之后，窃贼又发现了一个新的可以打劫的地方，**但这次所有的房子组成的区域比较奇怪，聪明的窃贼考察地形之后，发现这次的地形是一颗二叉树**。与前两次偷窃相似的是每个房子都存放着特定金额的钱。你面临的唯一约束条件是：**相邻的房子装着相互联系的防盗系统，且当相邻的两个房子同一天被打劫时，该系统会自动报警**。

算一算，如果今晚去打劫，你最多可以得到多少钱，当然在不触动报警装置的情况下。
 ### 样例说明
 **样例1**

```
输入:  {3,2,3,#,3,#,1}
输出: 7
解释:
最多能偷 3 + 3 + 1 = 7.
  3
 / \
2   3
 \   \ 
  3   1
```

**样例2**

```
输入:  {3,4,5,1,3,#,1}
输出: 9
解释:
最多能偷 4 + 5 = 9.
    3
   / \
  4   5
 / \   \ 
1   3   1
```
 ### 参考代码
 动态规划
首先枚举是否抢第一个房子
考虑前若干个房子，记录抢最后一个房子或者不抢最后一个房子能抢到的最多的钱
然后交叉更新
```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        sef.val = val
        self.left, self.right = None, None
"""
class Solution:
    # @param {TreeNode} root, the root of binary tree.
    # @return {int} The maximum amount of money you can rob tonight
    def houseRobber3(self, root):
        # write your code here
        rob, not_rob = self.visit(root)
        return max(rob, not_rob)
        
    def visit(self, root):
        if root is None:
            return 0, 0
        
        left_rob, left_not_rob = self.visit(root.left)
        right_rob, right_not_rob = self.visit(root.right)
        
        rob = root.val + left_not_rob + right_not_rob
        not_rob = max(left_rob, left_not_rob) + max(right_rob, right_not_rob)
        return rob, not_rob
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)