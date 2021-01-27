# 生成括号
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/generate-parentheses/?utm_source=sc-github-wzz)
 ## 题目描述
 给定 n，表示有 n 对括号, 请写一个函数以将其生成所有的括号组合，并返回组合结果。
 ### 样例说明
 **样例 1:**

```
输入: 3
输出: ["((()))", "(()())", "(())()", "()(())", "()()()"] 
```

**样例 2:**

```
输入: 2
输出: ["()()", "(())"]
```
 ### 参考代码
 回溯. 逐个字符添加, 生成每一种组合. 

一个状态需要记录的有: 当前字符串本身, 左括号数量, 右括号数量.

递归过程中解决:

- 如果当前右括号数量等于括号对数 n, 那么当前字符串即是一种组合, 放入解中.
- 如果当前左括号数量等于括号对数 n, 那么当前字符串后续填充满右括号, 即是一种组合.
- 如果当前左括号数量未超过 n:
  - 如果左括号多于右括号, 那么此时可以添加一个左括号或右括号, 递归进入下一层
  - 如果左括号不多于右括号, 那么此时只能添加一个左括号, 递归进入下一层
```java
public class Solution {
    public ArrayList<String> generateParenthesis(int n) {
        ArrayList<String> result = new ArrayList<String>();
        if (n <= 0) {
            return result;
        }
        helper(result, "", n, n);
        return result;
    }
    
	public void helper(ArrayList<String> result,
	                   String paren, // current paren
	                   int left,     // how many left paren we need to add
	                   int right) {  // how many right paren we need to add
		if (left == 0 && right == 0) {
			result.add(paren);
			return;
		}

        if (left > 0) {
		    helper(result, paren + "(", left - 1, right);
        }
        
        if (right > 0 && left < right) {
		    helper(result, paren + ")", left, right - 1);
        }
	}
}

///////////////////// 九章硅谷求职算法集训营版本

class Solution {
    List<String> res = new ArrayList<>();
    int n;
    
    void gen(int nleft, int nright, String cur) {
        if (nleft == n && nright == n) {
            res.add(cur);
            return;
        }
        
        if (nleft < n) {
            gen(nleft + 1, nright, cur + "(");
        }
        
        if (nright < nleft) {
            gen(nleft, nright + 1, cur + ")");
        }
    }
    
    public List<String> generateParenthesis(int nn) {
        n = nn;
        gen(0, 0, "");
        return res;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)