# 有效的括号序列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/valid-parentheses/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个字符串所表示的括号序列，包含以下字符： `'(', ')'`, `'{'`, `'}'`, `'['` and `']'`， 判定是否是有效的括号序列。

括号必须依照 `"()"` 顺序表示， `"()[]{}"` 是有效的括号，但 `"([)]"` 则是无效的括号。
 ### 样例说明
 
**样例 1：**
```
输入："([)]"
输出：False
```
**样例 2：**
```
输入："()[]{}"
输出：True
```

 ### 参考代码
 Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.&nbsp;
```java
public class Solution {
    public boolean isValidParentheses(String s) {
        Stack<Character> stack = new Stack<Character>();
        for (Character c : s.toCharArray()) {
	    if ("({[".contains(String.valueOf(c))) {
                stack.push(c);
            } else {
               if (!stack.isEmpty() && is_valid(stack.peek(), c)) {
                   stack.pop();
               } else {
                   return false;
               }
           }
       }
       return stack.isEmpty();
    }

    private boolean is_valid(char c1, char c2) {
        return (c1 == '(' && c2 == ')') || (c1 == '{' && c2 == '}')
            || (c1 == '[' && c2 == ']');
    }
}

// version: 高频题班
public class Solution {
    /**
     * @param s A string
     * @return whether the string is a valid parentheses
     */
    public boolean isValidParentheses(String s) {
        // Write your code here
        Stack<Character> stack = new Stack<>();
        for (char c : s.toCharArray()) {
            if (c == '(' || c == '[' || c == '{') {
                stack.push(c);
            }
            if (c == ')') {
                if (stack.isEmpty() || stack.pop() != '(') {
                    return false;
                }
            }
            if (c == ']') {
                if (stack.isEmpty() || stack.pop() != '[') {
                    return false;
                }
            }
            if (c == '}') {
                if (stack.isEmpty() || stack.pop() != '{') {
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }
}



```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)