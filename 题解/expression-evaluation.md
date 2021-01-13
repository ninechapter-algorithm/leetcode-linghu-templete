# 表达式求值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/expression-evaluation/?utm_source=sc-github-wzz)
 ## 题目描述
 给一个用字符串表示的表达式数组，求出这个表达式的值。

 ### 样例说明
 **样例 1:**
```
对于表达式 `2*6-(23+7)/(1+2)`,
输入:
["2", "*", "6", "-", "(","23", "+", "7", ")", "/", "(", "1", "+", "2", ")"]
输出:
2
```

**样例 2:**
```
对于表达式 `4-(2-3)*2+5/5`,
输入:
["4", "-", "(", "2","-", "3", ")", "*", "2", "+", "5", "/", "5"]
输出:
7
```
 ### 参考代码
 把表达式转为反波兰表达式，存入单调栈，根据优先级，弹出并进行计算
```java
class TreeNode {
	public int val;
	public String s;
	public TreeNode left, right;

	public TreeNode(int val, String ss) {
		this.val = val;
		this.s = ss;
		this.left = this.right = null;
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

	void dfs(TreeNode root, ArrayList<String> as) {
		if(root==null)
			return;
		if (root.left != null)
			dfs(root.left, as);
		
		if (root.right != null)
			dfs(root.right, as);
		as.add(root.s);
	}

	public int evaluateExpression(String[] expression) {
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
						right.left = nodeNow;

					} else {
						TreeNode left = stack.peek();
						if (left.val < right.val) {
							right.left = nodeNow;
						} else {
							left.right = nodeNow;
						}
					}
				} else {
					break;
				}
			}
			stack.push(right);
		}

		ArrayList<String> reversepolish = new ArrayList<String>();
		dfs(stack.peek().left, reversepolish);
		String[] str = new String[reversepolish.size()];
		reversepolish.toArray(str);
		//System.out.println(as);
		
		return evalreversepolish(str);
	}

	int evalreversepolish(String[] tokens) {
		int returnValue = 0;
		String operators = "+-*/";

		Stack<String> stack = new Stack<String>();

		for (String ss : tokens) {
			if (!operators.contains(ss)) {
				stack.push(ss);
			} else {
				int a = Integer.valueOf(stack.pop());
				int b = Integer.valueOf(stack.pop());
				if (ss.equals("+")) {
					stack.push(String.valueOf(a + b));
				} else if (ss.equals("-")) {
					stack.push(String.valueOf(b - a));
				} else if (ss.equals("*")) {
					stack.push(String.valueOf(a * b));
				} else if (ss.equals("/")) {
					stack.push(String.valueOf(b / a));
				}
			}
		}
		if(stack.isEmpty())
			returnValue = 0;
		else 
			returnValue = Integer.valueOf(stack.pop());

		return returnValue;
	}
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)