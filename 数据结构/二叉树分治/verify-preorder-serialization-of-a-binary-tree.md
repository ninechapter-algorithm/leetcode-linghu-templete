# 验证二叉树的前序序列化
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/verify-preorder-serialization-of-a-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 二叉树序列化的一种方法是使用先序遍历。 当我们遇到非空节点时，我们记录节点的值。如果是一个空节点，我们使用诸如#的标记值。
~~~~.
     _9_
    /   \
   3     2
  / \   / \
 4   1  #  6
/ \ / \   / \
# # # #   # #
~~~~
例如，上面的二叉树可以序列化为字符串”9,3,4,#,#,1,#,#,2,#,6,#,#”，其中#表示空节点。

给定一个用逗号分隔的字符串，验证它是否是二叉树序列化正确的前序遍历。 找到一个不需要重建树的算法。

字符串中的每个逗号分隔的值必须是整数或表示空指针的字符“#”。

您可以假设输入格式始终符合要求，例如它永远不能包含两个连续的逗号，例如“1,,3”。
 ### 样例说明
 ```
样例 1:
	输入:  tree = "#"
	输出:  true
	
	解释:
	空树是合法的BST。
	
样例 2:
	输入: tree = "9,3,4,#,#,1,#,#,2,#,6,#,#"
	输出:  true

样例 3:
	输入: tree = "1,#"
	输出:  false
	
	解释:
	不是一棵完整的树
	
样例 4:
	输入: tree = "9,#,#,1"
	输出:  false
	
	解释:
	不是一棵树

```

 ### 参考代码
 ```java
public class Solution {
    public boolean isValidSerialization(String preorder) {
        String s = preorder;
        boolean flag = true;
        while (s.length() > 1) {
            int index = s.indexOf(",#,#");
            if (index < 0) {
                flag = false;
                break;
            }
            int start = index;
            while (start > 0 && s.charAt(start - 1) != ',')
            {
                start --;
            }
            if (s.charAt(start) == '#') {
                flag = false;
                break;
            }
            s = s.substring(0, start) + s.substring(index + 3);
        }
        if (s.equals("#") && flag) 
            return true;
        else 
            return false;
    }
}



```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)