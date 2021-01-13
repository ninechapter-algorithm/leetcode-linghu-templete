# 二叉树垂直遍历
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-vertical-order-traversal/?utm_source=sc-github-wzz)
 ## 题目描述
 给定二叉树，返回其节点值的垂直遍历顺序。 (即逐列从上到下)。
如果两个节点在同一行和同一列中，则顺序应 **从左到右**。
 ### 样例说明
 **样例1**
```
输入： {3,9,20,#,#,15,7}
输出： [[9],[3,15],[20],[7]]
解释：
   3
  /\
 /  \
 9  20
    /\
   /  \
  15   7
```
**样例2**
```
输入： {3,9,8,4,0,1,7}
输出：[[4],[9],[3,0,1],[8],[7]]
解释：
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
```
 ### 参考代码
 对于一棵树，我们设其根节点的位置为0。
对于任一非叶子节点，若其位置为x，设其左儿子的位置为x-1，右儿子位置为x+1。
按照以上规则bfs遍历整棵树统计所有节点的位置，然后按位置从小到大输出所有节点。
```java
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
     * @param root the root of binary tree
     * @return the vertical order traversal
     */
    public List<List<Integer>> verticalOrder(TreeNode root) {
        // Write your code here
        List<List<Integer>> results = new ArrayList<>();
        if (root == null) {
            return results;
        }
        Map<Integer, List<Integer>> map = new TreeMap<Integer, List<Integer>>();
        Queue<Integer> qCol = new LinkedList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        qCol.offer(0);
        
        while(!queue.isEmpty()) {
            TreeNode curr = queue.poll();
            int col = qCol.poll();
            if(!map.containsKey(col)) {
                map.put(col, new ArrayList<Integer>(Arrays.asList(curr.val)));
            } else {
                map.get(col).add(curr.val);
            }
            if(curr.left != null) {
                queue.offer(curr.left);
                qCol.offer(col - 1);
            }
            if(curr.right != null) {
                queue.offer(curr.right);
                qCol.offer(col + 1);
            }
        }
        for(int n : map.keySet()) {
            results.add(map.get(n));
        }
        return results;
    }   
}

// version: 高频题班
public class Solution {
    /**
     * @param root the root of binary tree
     * @return the vertical order traversal
     */
    public List<List<Integer>> verticalOrder(TreeNode root) {
        // Write your code here
        List<List<Integer>> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }

        Map<Integer, List<Integer>> hash = new HashMap<>();
        Queue<Integer> qCol = new LinkedList<>();
        Queue<TreeNode> qNode = new LinkedList<>();

        qCol.offer(0);
        qNode.offer(root);

        while (!qCol.isEmpty()) {                      // bfs
            int c = qCol.poll();
            TreeNode node = qNode.poll();

            hash.putIfAbsent(c, new ArrayList<>());
            hash.get(c).add(node.val);

            if (node.left != null) {
                qCol.offer(c - 1);
                qNode.offer(node.left);
            }
            if (node.right != null) {
                qCol.offer(c + 1);
                qNode.offer(node.right);
            }
        }

        for (int i = Collections.min(hash.keySet()); i <= Collections.max(hash.keySet()); i++) {
            ans.add(hash.get(i));
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)