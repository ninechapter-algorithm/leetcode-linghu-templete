# 表达树构造
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/expression-tree-build/?utm_source=sc-github-wzz)
 ## 题目描述
 表达树是一个二叉树的结构，用于衡量特定的表达。所有表达树的叶子都有一个数字字符串值。而所有表达树的非叶子都有另一个操作字符串值。

给定一个表达数组，请构造该表达的表达树，并返回该表达树的根。
 ### 样例说明
 **样例 1:**
```
输入: ["2","*","6","-","(","23","+","7",")","/","(","1","+","2",")"]
输出: {[-],[*],[/],[2],[6],[+],[+],#,#,#,#,[23],[7],[1],[2]} 
解释:
其表达树如下：

	                 [ - ]
	             /          \
	        [ * ]              [ / ]
	      /     \           /         \
	    [ 2 ]  [ 6 ]      [ + ]        [ + ]
	                     /    \       /      \
	                   [ 23 ][ 7 ] [ 1 ]   [ 2 ] .

在构造该表达树后，你只需返回根节点`[-]`。
```

**样例 2:**
```
输入: ["10","+","(","3","-","5",")","+","7","*","7","-","2"]
输出: {[-],[+],[2],[+],[*],#,#,[10],[-],[7],[7],#,#,[3],[5]}
解释:
其表达树如下：
 	                       [ - ]
	                   /          \
	               [ + ]          [ 2 ]
	           /          \      
	       [ + ]          [ * ]
              /     \         /     \
	  [ 10 ]  [ - ]    [ 7 ]   [ 7 ]
	          /    \ 
                [3]    [5]
在构造该表达树后，你只需返回根节点`[-]`。
```

 ### 参考代码
 根据运算符的优先级来构造单调递增栈，最后弹出栈中元素，最后一个就是根节点，返回即可。
```java
// version 1
/**
 * Definition of ExpressionTreeNode:
 * public class ExpressionTreeNode {
 *     public String symbol;
 *     public ExpressionTreeNode left, right;
 *     public ExpressionTreeNode(String symbol) {
 *         this.symbol = symbol;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    class TreeNode {
        int val;
        ExpressionTreeNode eNode;
        public TreeNode(int val, String s) {
            this.val = val;
            eNode = new ExpressionTreeNode(s);
        }
    }
    /**
     * @param expression: A string array
     * @return: The root of expression tree
     */
    public ExpressionTreeNode build(String[] expression) {
        if (expression == null || expression.length == 0) {
            return null;
        }
        Stack<TreeNode> stack = new Stack<TreeNode>();
        int base = 0;
        int val = 0;

        for (int i = 0; i < expression.length; i++) {
            if (expression[i].equals("(")) {
                base += 10;
                continue;
            }
            if (expression[i].equals(")")) {
                base -= 10;
                continue;
            }
            val = getWeight(base, expression[i]);
            TreeNode node = new TreeNode(val, expression[i]);
            while (!stack.isEmpty() && node.val <= stack.peek().val) {
                node.eNode.left = stack.pop().eNode;
            }
            if (!stack.isEmpty()) {
                stack.peek().eNode.right = node.eNode;
            }
            stack.push(node);
        }
        if (stack.isEmpty()) {
            return null;
        }
        TreeNode rst = stack.pop();
        while (!stack.isEmpty()) {
            rst = stack.pop();
        }
        return rst.eNode;
    }
    //Calculate weight for characters
    public int getWeight(int base, String s) {
        if (s.equals("+") || s.equals("-")) {
            return base + 1;
        }
        if (s.equals("*") || s.equals("/")) {
            return base + 2;
        }
        return Integer.MAX_VALUE;
    }
}

// version 2
/**
 * Definition of ExpressionTreeNode:
 * public class ExpressionTreeNode {
 *     public String symbol;
 *     public ExpressionTreeNode left, right;
 *     public ExpressionTreeNode(rooting symbol) {
 *         this.symbol = symbol;
 *         this.left = this.right = null;
 *     }
 * }
 */
class TreeNode {
	public int val;
	public String s;
	public ExpressionTreeNode root; 

	public TreeNode(int val, String ss) {
		this.val = val;
		this.root = new ExpressionTreeNode(ss);
	}

}

public class Solution {

	int get(String a, Integer base) {
		if (a.equals("+") || a.equals("-"))
			return 1 + base;
		if (a.equals("*") || a.equals("/"))
			return 2 + base;

		return Integer.MAX_VALUE;
	}



	public ExpressionTreeNode build(String[] expression) {
		// write your code here
		Stack<TreeNode> stack = new Stack<TreeNode>();
		TreeNode root = null;
		int val = 0;
		Integer base = 0;
		for (int i = 0; i <= expression.length; i++) {
			if(i != expression.length)
			{
				
				if (expression[i].equals("(")) {
					base += 10;
					continue;
				}
				if (expression[i].equals(")")) {
					base -= 10;
					continue;
				}
				val = get(expression[i], base);

			}
			TreeNode right = i == expression.length ? new TreeNode(
					Integer.MIN_VALUE, "") : new TreeNode(val,
					expression[i]);
			while (!stack.isEmpty()) {
				if (right.val <= stack.peek().val) {
					TreeNode nodeNow = stack.pop();

					if (stack.isEmpty()) {
						right.root.left = nodeNow.root;

					} else {
						TreeNode left = stack.peek();
						if (left.val < right.val) {
							right.root.left = nodeNow.root;
						} else {
							left.root.right = nodeNow.root;
						}
					}
				} else {
					break;
				}
			}
			stack.push(right);
		}

	
		
		return stack.peek().root.left;
	}


};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)